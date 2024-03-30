<script>
	import { onMount } from 'svelte';
	import { scaleLinear, scaleOrdinal, stack, area, curveBasis } from 'd3';
	import { csv } from 'd3-fetch';
	import * as d3 from 'd3';
	let data = [];
	$: selectedCategory = 'Colorwork'; // Default category
	$: stackedAreas = [];
	$: filteredData = [];

	const margin = { top: 20, right: 30, bottom: 30, left: 60 };
	const width = 600 - margin.left - margin.right;
	const height = 400 - margin.top - margin.bottom;

	$: categories = [...new Set(data.map((d) => d.category))];

	onMount(async () => {
		data = await csv(
			'../data/tags_data_for_d3.csv',
			({ category, year, tags, tag_count }) => ({
				category,
				year: +year,
				tag: tags,
				count: +tag_count,
			}),
		);
	});

	$: {
		renderChart(selectedCategory);
	}

	let renderChart = (selectedCategory) => {
		filteredData = data.filter((d) => d.category === selectedCategory);
		if (filteredData.length === 0) {
			// Handle the case when there's no data for the selected category
			stackedAreas = [];
			return;
		}

		// const x = scaleLinear().domain([2013, 2023]).range([0, width]);

		// let maxY = d3.max(filteredData, (d) => d.count);
		// maxY = maxY === undefined ? 0 : maxY;
		// console.log(maxY);

		// const y = scaleLinear().domain([0, 10000]).range([height, 0]);
		if (filteredData.length > 0) {
			const x = scaleLinear()
				.domain(d3.extent(filteredData, (d) => d.year))
				.range([0, width]);

			console.log('X Scale Domain:', x.domain());

			console.log('filteredData', filteredData);
			// const yMax = d3.max(filteredData, (d) => d.count);

			const colors = scaleOrdinal(d3.schemeCategory10);

			// const stackData = d3
			// 	.stack()
			// 	.keys(Array.from(new Set(filteredData.map((d) => d.tag))))(filteredData);
			const keys = Array.from(new Set(filteredData.map((d) => d.tag)));
			console.log('filtered data', filteredData);
			// const stackData = d3
			// 	.stack()
			// 	.keys(d3.union(filteredData.map((d) => d.tag)))
			// 	.value(([, group], key) => {
			// 		// return group.get(key)?.count || 0;
			// 		return group.get(key)?.count;
			// 	})(
			// 	d3.index(
			// 		filteredData,
			// 		(d) => d.year,
			// 		(d) => d.tag,
			// 	),
			// );

			const stackData = d3
				.stack()
				.keys(d3.union(filteredData.map((d) => d.tag)))
				.order(d3.stackOrderAscending)
				.value(([, group], key) => {
					return group.get(key)?.count;
				})(
				d3.index(
					filteredData,
					(d) => {
						return d.year;
					},
					(d) => {
						return d.tag;
					},
				),
			);
			console.log('stack data', stackData);
			console.log(typeof stackData);

			// const areaGenerator = area()
			// 	.x((d) => {
			// 		console.log(d);
			// 		return x(d.data.year);
			// 	})
			// 	.y0((d) => y(d[0]))
			// 	.y1((d) => y(d[1]));

			// Group data by year and sum tag_count for each year
			const nestedData = d3.rollup(
				filteredData,
				(v) => d3.sum(v, (d) => d.count),
				(d) => d.year,
			);
			console.log('nested', nestedData);
			console.log('nested', d3.max(nestedData));

			let highestSum = 0;

			for (const [year, sum] of nestedData.entries()) {
				if (sum > highestSum) {
					highestSum = sum;
				}
			}

			const y = scaleLinear().domain([0, highestSum]).nice().range([height, 0]);

			const areaGenerator = d3
				.area()
				.x((d) => {
					// Check if x scale is defined and initialized
					// return x && d.data && d.data.year ? x(d.data.year) : 10;
					return x(d.data[0]);
					// return x(d.data.year);
				})
				.y0((d) => {
					// Check if y scale is defined and initialized
					// return y && d && d[0] ? y(d[1]) : 10;
					return d[0] ? y(d[0]) : y(0);
				})
				.y1((d) => {
					// Check if y scale is defined and initialized
					return d[1] ? y(d[1]) : y(0);
					// return Math.abs(y(d[1]));
				})
				.curve(d3.curveBasis);

			console.log('layers');
			stackData.map((layer) => console.log(layer));
			stackedAreas = stackData.map((layer, i) => ({
				path: areaGenerator(layer),
				color: colors(layer.key),
			}));

			console.log('number of areas', stackedAreas.length);

			console.log('stacked areas', stackedAreas);
		}
	};
</script>

<h1>Current category {selectedCategory}</h1>
<select bind:value={selectedCategory}>
	{#each categories as cat}
		<option value={cat}>{cat}</option>
	{/each}
</select>
<div>
	{#if data.length > 0 && filteredData.length > 0}
		<svg
			width="1000"
			height="1000"
		>
			<g transform={`translate(${margin.left},${margin.top})`}>
				{#each stackedAreas as { path, color }, i}
					<path
						d={path}
						fill={color}
					/>
				{/each}
			</g>
		</svg>
	{/if}
</div>

<style>
	.x-axis line,
	.x-axis path {
		fill: none;
		stroke: #000;
		shape-rendering: crispEdges;
	}

	.y-axis line,
	.y-axis path {
		fill: none;
		stroke: #000;
		shape-rendering: crispEdges;
	}
</style>

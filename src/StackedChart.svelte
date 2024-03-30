<script>
	import { onMount } from 'svelte';
	import { csv } from 'd3-fetch';
	import * as d3 from 'd3';

	let data = [];
	$: selectedCategory = 'Colorwork';
	$: stackedAreas = [];
	$: filteredData = [];
	$: textLabels = [];

	const container_width = 1000;
	const container_height = 600;

	const margin = { top: 20, right: 150, bottom: 30, left: 60 };
	const width = container_width - margin.left - margin.right;
	const height = container_height - margin.top - margin.bottom;

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
		renderChart(selectedCategory);
	});

	$: {
		renderChart(selectedCategory);
	}

	let renderChart = (selectedCategory) => {
		filteredData = data.filter((d) => d.category === selectedCategory);
		if (filteredData.length === 0) {
			stackedAreas = [];
			return;
		}

		if (filteredData.length > 0) {
			const x = d3
				.scaleLinear()
				.domain(d3.extent(filteredData, (d) => d.year))
				.range([0, width]);

			const colors = d3.scaleOrdinal(d3.schemeCategory10);

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

			// group data by year and sum tag_count for each year
			const nestedData = d3.rollup(
				filteredData,
				(v) => d3.sum(v, (d) => d.count),
				(d) => d.year,
			);

			let highestSum = 0;

			// calculate "tallest" year for y-axis
			// need "year" here to deconstruct entries correctly
			for (const [year, sum] of nestedData.entries()) {
				if (sum > highestSum) {
					highestSum = sum;
				}
			}

			const y = d3
				.scaleLinear()
				.domain([0, highestSum])
				.nice()
				.range([height, 0]);

			const areaGenerator = d3
				.area()
				.x((d) => {
					return x(d.data[0]);
				})
				.y0((d) => {
					return d[0] ? y(d[0]) : y(0);
				})
				.y1((d) => {
					return d[1] ? y(d[1]) : y(0);
				})
				.curve(d3.curveBasis);

			stackedAreas = stackData.map((layer, i) => ({
				path: areaGenerator(layer),
				color: colors(layer.key),
			}));

			const top3Areas = stackData
				.map((layer, i) => ({
					area: layer,
					sum: d3.sum(layer, (d) => d[1] - d[0]),
				}))
				.sort((a, b) => b.sum - a.sum);

			console.log('top3 areas', top3Areas);

			let midpoints = top3Areas.map(({ area }, i) => {
				let lastArea = area[area.length - 1];
				return (lastArea[0] + lastArea[1]) / 2;
			});

			// only show labels when area height > threshold
			textLabels = top3Areas
				.filter(({ area }) => {
					let lastArea = area[area.length - 1];
					return lastArea[1] - lastArea[0] > 80;
				})
				.map(({ area }, i) => ({
					label: area.key,
					x: width + 65,
					y: y(midpoints[i]) + margin.top,
					color: colors(area.key),
				}));
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
			width={container_width}
			height={container_height}
		>
			<g transform={`translate(${margin.left},${margin.top})`}>
				{#each stackedAreas as { path, color }, i}
					<path
						d={path}
						fill={color}
					/>
				{/each}
			</g>
			{#each textLabels as { label, x, y, color }}
				<text
					x={x}
					y={y}
					fill="black"
					text-anchor="start"
				>
					{label}
				</text>
			{/each}
		</svg>
	{/if}
</div>

<style>
	text {
		font-family: Helvetica, sans-serif;
	}
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

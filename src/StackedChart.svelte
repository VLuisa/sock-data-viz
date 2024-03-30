<script>
	import { onMount } from 'svelte';
	import { csv } from 'd3-fetch';
	import * as d3 from 'd3';

	let data = [];
	$: selectedCategory = 'Heel';
	$: stackedAreas = [];
	$: filteredData = [];
	$: textLabels = [];

	$: gx = null;
	$: x = null;
	$: {
		if (x != null && gx != null) {
			const formatYear = d3.format('d');

			d3.select(gx)
				.call(d3.axisBottom(x).tickFormat(formatYear))
				.select('.domain')
				.attr('opacity', '0');

			d3.select(gx).selectAll('.tick line').remove();
		}
	}

	const lightGray = '#D6D2CB';
	const darkGray = '#7F7B74';
	const colors = {
		Heel: '#F0439F',
		Toe: '#FFB629',
		Colorwork: '#2B5C63',
		'Fabric / Stitches': '#21ACCA',
		'Sock Method': '#CB82DA',
	};

	const container_width = 1000;
	const container_height = 600;

	const margin = { top: 20, right: 150, bottom: 30, left: 60 };
	const width = container_width - margin.left - margin.right;
	const height = container_height - margin.top - margin.bottom;

	$: categories = [
		'Heel',
		'Toe',
		'Sock Method',
		'Colorwork',
		'Fabric / Stitches',
	];

	onMount(async () => {
		data = await csv(
			'../data/tags_data_for_d3.csv',
			({ category, year, tag_count, tags, clean_name }) => ({
				category,
				year: +year,
				count: +tag_count,
				tag: clean_name,
			}),
		);
		renderChart(selectedCategory);
	});

	let renderChart = (selectedCategory) => {
		filteredData = data.filter((d) => d.category === selectedCategory);
		if (filteredData.length === 0) {
			stackedAreas = [];
			return;
		}

		if (filteredData.length > 0) {
			x = d3
				.scaleLinear()
				.domain(d3.extent(filteredData, (d) => d.year))
				.range([0, width]);

			const stackData = d3
				.stack()
				.keys(d3.union(filteredData.map((d) => d.tag)))
				.order(d3.stackOrderAscending)
				.value(([, group], key) => {
					return group.get(key)?.count;
				})(
				d3.index(
					filteredData,
					(d) => d.year,
					(d) => d.tag,
				),
			);

			const topAreas = stackData
				.map((layer, i) => ({
					area: layer,
					sum: d3.sum(layer, (d) => d[1] - d[0]),
				}))
				.sort((a, b) => b.sum - a.sum);

			const categoryColor = colors[selectedCategory];
			const opacityStep = 1 / stackData.length;

			const opacityMap = new Map();
			topAreas.forEach((area, i) => {
				opacityMap.set(area.area.key, 1 - i * opacityStep);
			});

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
				color: categoryColor,
				opacity: opacityMap.get(layer.key),
			}));

			let midpoints = topAreas.map(({ area }, i) => {
				let lastArea = area[area.length - 1];
				return (lastArea[0] + lastArea[1]) / 2;
			});

			// only show labels when area height > threshold
			textLabels = topAreas
				.filter(({ area }) => {
					let lastArea = area[area.length - 1];
					return lastArea[1] - lastArea[0] > 80;
				})
				.map(({ area }, i) => ({
					label: area.key,
					x: width + 65,
					y: y(midpoints[i]) + margin.top,
					color: categoryColor,
				}));
		}
	};
</script>

<div class="chart-container">
	<div
		class="tab-container"
		style="width: {container_width}"
	>
		{#each categories as cat}
			<button
				class:active={selectedCategory === cat}
				style="--active-color: {colors[selectedCategory]}; }"
				on:click={() => {
					selectedCategory = cat;
					renderChart(selectedCategory);
				}}
				class="tab"
			>
				{cat}
			</button>
		{/each}
	</div>
	<div>
		{#if data.length > 0 && filteredData.length > 0}
			<svg
				width={container_width}
				height={container_height}
			>
				<g transform={`translate(${margin.left},${margin.top})`}>
					{#each stackedAreas as { path, color, opacity }, i}
						<path
							d={path}
							fill={color}
							opacity={opacity}
						/>
					{/each}
				</g>
				{#each textLabels as { label, x, y, color }}
					<text
						x={x}
						y={y}
						fill={color}
						text-anchor="start"
					>
						{label}
					</text>
				{/each}
				<g
					class="x-axis"
					transform={`translate(${margin.left}, ${height + margin.top})`}
					bind:this={gx}
					style={`font-size: 0.9em; color: ${darkGray}`}
				></g>
			</svg>
		{/if}
	</div>
</div>

<style>
	.chart-container {
		display: flex;
		flex-flow: column nowrap;
		align-items: center;
		width: 100%;
	}
	text {
		font-family: Helvetica, sans-serif;
	}

	path {
		transition: 0.3s ease-out;
		stroke: white;
	}

	.tab-container {
		display: flex;
		justify-content: stretch;
		width: 1000px; /* should match container width */
	}

	button {
		padding: 10px 20px;
		margin: 0 5px;
		border: none;
		background-color: transparent;
		cursor: pointer;
		font-size: 16px;
		color: #7f7b74; /* dark gray from style*/
		border-radius: 10px;
	}

	.tab {
		display: inline-block;
		padding: 10px 20px;
		cursor: pointer;
		font-size: 16px;
		position: relative;
		width: 100%;
	}

	.active {
		color: black;
		background-color: var(--active-color);
	}
</style>

<script>
	import { onMount } from 'svelte';
	import { csv } from 'd3-fetch';
	import * as d3 from 'd3';
	import MiniSockImage from './MiniSockImage.svelte';
	import { COLORS, DARK_GRAY } from './constants';

	let data = [];
	$: selectedCategory = 'Heel';
	$: stackedAreas = [];
	$: filteredData = [];
	$: textLabels = [];

	let narrowWindow = 600;

	$: tickCount = container_width < narrowWindow ? 4 : 10;

	$: gx = null;

	$: {
		if (xScale) {
			renderChart(selectedCategory);
		}
	}
	$: xScale =
		filteredData?.length > 0
			? d3
					.scaleLinear()
					.domain(d3.extent(filteredData, (d) => d.year))
					.range([0, width])
			: null;

	$: yScale = null;
	$: {
		if (xScale != null && gx != null) {
			const formatYear = d3.format('d');

			d3.select(gx)
				.call(d3.axisBottom(xScale).tickFormat(formatYear).ticks(tickCount))
				.select('.domain')
				.attr('opacity', '0');

			d3.select(gx).selectAll('.tick line').remove();
		}
	}

	$: container_width = 700;
	const container_height = 400;

	$: right_margin = container_width > narrowWindow ? 300 : 200;

	let margin = { top: 20, right: 0, bottom: 30, left: 20 };
	$: {
		margin.right = right_margin;
	}
	$: width = container_width - margin.left - margin.right;
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
			'/data/tags data for d3 - 1.csv',
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

		if (filteredData.length > 0 && xScale != null) {
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

			const categoryColor = COLORS[selectedCategory];
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

			yScale = d3
				.scaleLinear()
				.domain([0, highestSum])
				.nice()
				.range([height, 0]);

			const areaGenerator = d3
				.area()
				.x((d) => {
					return xScale(d.data[0]);
				})
				.y0((d) => {
					return d[0] ? yScale(d[0]) : yScale(0);
				})
				.y1((d) => {
					return d[1] ? yScale(d[1]) : yScale(0);
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
					x: width + margin.left + 5,
					y: yScale(midpoints[i]) + margin.top,
					color: categoryColor,
				}));
		}
	};
</script>

<div class="matrix-title">
	<h2>What can go into knitting a sock?</h2>
	<p>
		Explore the most popular sock techniques over the years. See trends of the
		most popular parts of a sock. Maybe find a new technique to try for your
		first (or next) pair of socks.
	</p>
	<div class="spacer-small" />
	{#if container_width < narrowWindow}
		<h5>Select a different category to see tag trends over the years.</h5>
	{:else}
		<h5>Click these buttons to see tag trends in different categories.</h5>
	{/if}

	<div class="spacer-small" />
</div>
<div class="chart-container">
	<div
		class="tab-container"
		style="width: {container_width}"
	>
		{#if container_width < narrowWindow}
			<select
				style="--active-color: {COLORS[selectedCategory]};"
				bind:value={selectedCategory}
				on:change={() => {
					renderChart(selectedCategory);
				}}
			>
				{#each categories as cat}
					<option value={cat}>{cat}</option>
				{/each}
			</select>
		{:else}
			{#each categories as cat}
				<button
					class:active={selectedCategory === cat}
					style="--active-color: {COLORS[selectedCategory]};"
					on:click={() => {
						selectedCategory = cat;
						renderChart(selectedCategory);
					}}
					class="tab"
				>
					{cat}
				</button>
			{/each}
		{/if}
	</div>

	<div
		class="component-body"
		bind:clientWidth={container_width}
	>
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
					style={`font-size: 0.9em; color: ${DARK_GRAY}`}
				></g>
			</svg>
		{/if}
		<MiniSockImage
			category={selectedCategory}
			width={container_width < narrowWindow ? 100 : 150}
		/>
	</div>
	<div class="spacer-medium" />
	<p class="footnote">
		Note: Some patterns use more than one technique (e.g. a pattern may be
		marked with both a "heel flap" and "short row" heel). From my digging this
		tended to be used when the pattern author was leaving it up to the reader to
		create the heel of their choice. More rarely, it meant they explained
		multiple heel types in the pattern.
	</p>
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
		font-size: calc(0.7em + 0.1vw);
	}

	path {
		transition: fill 0.5s ease-out;
		stroke: white;
	}

	.tab-container {
		display: flex;
		justify-content: stretch;
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
		border: 1px solid #7f7b74;
		transition: 0.3s ease-out;
	}

	.tab {
		display: inline-block;
		padding: 10px 20px;
		cursor: pointer;
		font-size: 16px;
		position: relative;
		width: 100%;
		line-height: 0.9em;
	}

	.active {
		color: var(--white);
		background-color: var(--active-color);
		border: none;
	}

	.component-body {
		display: flex;
		flex-flow: row nowrap;
		flex-direction: row-reverse;
		width: 80vw;
	}

	/* Style for dropdown */
	select {
		padding: 10px;
		margin: 0 5px 5px;
		border: none;
		background-color: transparent;
		cursor: pointer;
		font-size: 16px;
		font-weight: bold;
		color: var(--white); /* dark gray from style*/
		border-radius: 10px;
		transition: 0.3s ease-out;
		width: 80vw;
		background-color: var(--active-color);
		border-right: 16px solid transparent;
	}
</style>

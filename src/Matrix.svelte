<script>
	import { onMount } from 'svelte';
	import { csv } from 'd3-fetch';
	import * as d3 from 'd3';

	import { ALL_COLORS, DARK_GRAY } from './constants.js';

	const container_width = 800;
	const container_height = 800;
	const margin = { top: 200, right: 100, bottom: 30, left: 200 };
	const width = container_width - margin.left - margin.right;
	const height = container_height - margin.top - margin.bottom;

	$: data = [];

	$: xScale = null;
	$: gx = null;

	$: yScale = null;
	$: gy = null;

	$: colorScale = null;

	$: {
		if (xScale != null && gx != null) {
			d3.select(gx)
				.call(d3.axisTop(xScale))
				.select('.domain')
				.attr('opacity', '0.5');

			// d3.select(gx)
			// 	.selectAll('.tick text')
			// 	.attr('transform', 'rotate(-45)')
			// 	.style('text-anchor', 'start')
			// 	.attr('dy', '0.4em')
			// 	.attr('dx', '0.7em');
			d3.select(gx).selectAll('.tick line').remove();
		}
	}

	$: {
		if (yScale != null && gy != null) {
			d3.select(gy)
				.call(d3.axisLeft(yScale))
				.select('.domain')
				.attr('opacity', '0.5');
		}

		d3.select(gy).selectAll('.tick line').remove();
	}

	$: activeColumn = 1;
	$: hoverColumn = null;

	const axisStyle = `font-size: 1em; color: ${DARK_GRAY}; font-family: 'Helvetica'; font-weight: normal`;

	onMount(async () => {
		data = await csv(
			'/data/top_20_profiles.csv',
			({ name, tags, category, order_no, tag_freq }, i) => ({
				category,
				title: order_no,
				tag: tags,
				order: +order_no,
				tag_freq,
			}),
		);
		renderChart();
	});

	let renderChart = () => {
		if (data != []) {
			data.sort((a, b) => b.tag_freq - a.tag_freq);

			const titles = data.map((d) => d.title);
			const tags = data.map((d) => d.tag);

			titles.sort((a, b) => {
				return (
					data.find((item) => item.title === a).order -
					data.find((item) => item.title === b).order
				);
			});

			xScale = d3.scaleBand().domain(titles).range([0, width]);
			yScale = d3.scaleBand().domain(tags).range([0, height]);

			const colorArray = Object.entries(ALL_COLORS).map(
				([category, color]) => ({ category, color }),
			);

			colorScale = d3
				.scaleOrdinal()
				.domain(colorArray.map((d) => d.category))
				.range(colorArray.map((d) => d.color));
		}
	};
</script>

{#if data.length > 0}
	<svg
		width={container_width}
		height={container_height}
	>
		{#if data.length > 0}
			{#each data as d}
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<rect
					x={xScale(d.title) + margin.left}
					y={yScale(d.tag) + margin.top}
					width={xScale.bandwidth()}
					height={yScale.bandwidth()}
					fill={colorScale(d.category)}
					on:click={() => {
						console.log('click', d.title);
						console.log('xscale', xScale(d.title));
						activeColumn = d.order;
					}}
					on:mouseenter={() => {
						console.log('hover', d.title);
						hoverColumn = d.order;
					}}
				/>
			{/each}

			<!-- Draw grid -->
			{#each yScale.domain() as tickY}
				<line
					x1={margin.left}
					x2={width + margin.left}
					y1={yScale(tickY) + yScale.bandwidth() + margin.top}
					y2={yScale(tickY) + yScale.bandwidth() + margin.top}
					style="stroke: {DARK_GRAY}; stroke-width: 1px;"
				/>
			{/each}
			{#each xScale.domain() as tickX}
				<line
					x1={xScale(tickX) + xScale.bandwidth() + margin.left}
					x2={xScale(tickX) + xScale.bandwidth() + margin.left}
					y1={margin.top}
					y2={height + margin.top}
					style="stroke: {DARK_GRAY}; stroke-width: 1px;"
				/>
			{/each}

			<g
				class="x-axis"
				transform={`translate(${margin.left}, ${margin.top})`}
				bind:this={gx}
				style={axisStyle}
			></g>
			<g
				class="y-axis"
				transform={`translate(${margin.left}, ${margin.top})`}
				bind:this={gy}
				style={axisStyle}
			>
			</g>
			<!-- Hover over item -->
			<!-- svelte-ignore a11y-no-static-element-interactions -->
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			{#if hoverColumn !== null}
				<rect
					x={xScale(xScale.domain()[hoverColumn - 1]) + margin.left}
					y={margin.top}
					width={xScale.bandwidth()}
					height={height}
					fill="white"
					opacity="0.2"
					on:click={() => {
						activeColumn = hoverColumn;
					}}
					class="hover-item"
				/>
			{/if}
			<!-- Highlight clicked item -->
			{#if activeColumn !== null && activeColumn >= 0}
				<rect
					x={xScale(xScale.domain()[activeColumn - 1]) + margin.left}
					y={margin.top}
					width={xScale.bandwidth()}
					fill="none"
					height={height}
					stroke={DARK_GRAY}
					stroke-width="5px"
					class="active-item"
				/>
			{/if}
		{/if}
	</svg>
{/if}

<style>
	.active-item {
		transition: 300ms ease-out;
	}
	.hover-item {
		transition: 50ms ease-in;
	}
</style>

<script>
	import { onMount } from 'svelte';
	import { csv } from 'd3-fetch';
	import * as d3 from 'd3';

	import { ALL_COLORS } from './constants.js';

	const container_width = 1000;
	const container_height = 1000;
	const margin = { top: 20, right: 20, bottom: 30, left: 30 };
	const width = container_width - margin.left - margin.right;
	const height = container_height - margin.top - margin.bottom;

	$: data = [];

	$: xScale = null;
	$: yScale = null;
	$: colorScale = null;

	onMount(async () => {
		data = await csv(
			'/data/top_20_profiles.csv',
			({ name, tags, category }) => ({
				category,
				title: name,
				tag: tags,
			}),
		);
		renderChart();
	});

	let renderChart = () => {
		if (data != []) {
			console.log(ALL_COLORS);

			const titles = data.map((d) => d.title);
			const tags = data.map((d) => d.tag);

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
				<rect
					x={xScale(d.title) + margin.left}
					y={yScale(d.tag) + margin.top}
					width={xScale.bandwidth()}
					height={yScale.bandwidth()}
					fill={colorScale(d.category)}
				/>
			{/each}
		{/if}
	</svg>
{/if}

<style>
</style>

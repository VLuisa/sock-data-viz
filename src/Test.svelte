<script>
	import * as d3 from 'd3';
	import { onMount } from 'svelte';
	import { scaleLinear } from 'd3-scale';
	import { stack, stackOffsetSilhouette } from 'd3-shape';
	import Label from './Label.svelte';

	// set the dimensions and margins of the graph
	const margin = { top: 300, right: 200, bottom: 30, left: 60 };
	const width = 600;
	const height = 500;

	let data;
	let y;
	let x;
	let maxY;
	$: stackedData = [];
	$: console.log(stackedData);
	$: keys = [];

	// color palette
	$: colorScale = d3
		.scaleOrdinal()
		.domain(keys)
		.range([
			'#e41a1c',
			'#377eb8',
			'#4daf4a',
			'#984ea3',
			'#ff7f00',
			'#ffff33',
			'#a65628',
			'#f781bf',
		]);

	$: console.log('Data', data);
	$: console.log('keys', keys);

	let activeIndex = ; // Index of the currently hovered area path

	// Function to handle mouseenter event
	function handleMouseEnter(index) {
		activeIndex = index; // Set activeIndex to the index of the hovered area path
	}

	// Function to handle mouseleave event
	function handleMouseLeave() {
		activeIndex = null; // Reset activeIndex when mouse leaves the area path
	}

	onMount(async () => {
		// Load CSV data
		const response = await fetch('../data/Tag lookup table - OnlyHeels.csv');
		const csvData = await response.text();

		// Parse CSV data
		data = d3.csvParse(csvData, d3.autoType);

		// List of groups = header of the csv files
		keys = data.columns.slice(2);

		// stack the data and sort the stacks from largest to smallest values
		stackedData = d3
			.stack()
			.keys(keys)
			.order(d3.stackOrderAscending) // sort stacks from largest to smallest values
			.offset(d3.stackOffsetNone)(
			// no offset, just summing values
			data,
		);

		// Calculate maxY dynamically
		maxY = d3.max(data.flatMap((d) => keys.map((k) => d[k])));

		console.log('maxY', maxY);

		// Add X axis
		x = scaleLinear()
			.domain(d3.extent(data, (d) => d.year))
			.range([0, width]);

		// Add Y axis
		y = scaleLinear()
			.domain([0, maxY])
			.range([height - margin.top - margin.bottom, 0]);

		// Update SVG elements
		stackedData.forEach((layer) => {
			layer.pathData = d3
				.area()
				.x((d, i) => x(d.data.year))
				.y0((d) => y(d[0]))
				.y1((d) => y(d[1]))(layer);

			// Bind data to path element
			layer.hoverData = layer;
		});
	});
</script>

<svg
	width={width + margin.left + margin.right}
	height={height + margin.top + margin.bottom}
>
	<g transform={`translate(${margin.left}, ${margin.top})`}>
		{#each stackedData as layer, index}
			<path
				d={layer.pathData}
				fill={colorScale(layer.key)}
				on:mouseenter={() => handleMouseEnter(index)}
				on:mouseleave={handleMouseLeave}
			/>
			{#if activeIndex === index && layer[0][1] - layer[0][0] > 0}
				<!-- Add Label component -->
				{console.log('layer', layer)}
				<Label
					x={width + 10}
					y={y(layer[0][1])}
					text={layer.key}
					color={colorScale(layer.key)}
					visible={true}
				/>
			{/if}
		{/each}
	</g>
</svg>

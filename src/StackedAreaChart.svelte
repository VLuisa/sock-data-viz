<script>
	import * as d3 from 'd3';
	import { scaleLinear } from 'd3-scale';
	import { stack } from 'd3-shape';
	import { onMount } from 'svelte';
	import Label from './Label.svelte';

	export let data;

	let y;
	let x;
	let maxY;
	let stackedData = [];
	let keys = [];

	let colorScale;
	let activeIndex = null;

	// set the dimensions and margins of the graph
	const margin = { top: 200, right: 200, bottom: 30, left: 60 };
	const width = 600;
	const height = 600;

	// Function to calculate maxY
	function calculateMaxY(data) {
		let max = 0;
		data.forEach((obj) => {
			Object.keys(obj).forEach((key) => {
				if (key !== 'year') {
					max = Math.max(max, obj[key]);
				}
			});
		});
		return max;
	}

	// This function initializes the necessary variables when data changes
	function processData(data) {
		if (data) {
			keys = Array.from(
				new Set(
					data.flatMap((d) => Object.keys(d)).filter((key) => key !== 'year'),
				),
			);

			console.log('keys', keys);
			stackedData = d3
				.stack()
				.keys(keys)
				.order(d3.stackOrderAscending)
				.offset(d3.stackOffsetNone)(data);
			maxY = calculateMaxY(data);
			console.log('maxY', maxY);

			x = scaleLinear()
				.domain(d3.extent(data, (d) => d.year))
				.range([0, width]);

			y = scaleLinear()
				.domain([0, maxY])
				.range([height - margin.top - margin.bottom, 0]);

			colorScale = d3
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

			console.log('stacked data', stackedData);
		}
	}

	// Call processData function when data changes
	$: processData(data);

	// Function to handle mouseenter event
	function handleMouseEnter(index) {
		activeIndex = index;
	}

	// Function to handle mouseleave event
	function handleMouseLeave() {
		activeIndex = null;
	}
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

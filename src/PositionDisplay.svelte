<script>
	import { scaleLinear } from 'd3-scale';
	import { DARK_GRAY, LIGHT_GRAY } from './constants';

	const width = 100;
	const height = 20;
	const barWidth = 100;
	const barHeight = 15;
	const margin = { top: 0, right: 5, bottom: 0, left: 5 };

	export let difficulty;
	export let outOf;

	$: xScale = scaleLinear()
		.domain([1, outOf])
		.range([margin.left, barWidth - margin.right]);
</script>

<svg
	width={width}
	height={height}
>
	<g transform="translate(0,0)">
		<!-- Horizontal bar -->
		<rect
			x={xScale(1)}
			y="5"
			width={xScale(10) - xScale(1)}
			height={barHeight}
			fill={LIGHT_GRAY}
		/>
		<rect
			x={xScale(difficulty)}
			y="5"
			width="5"
			height={barHeight}
			fill={DARK_GRAY}
		/>
	</g>
</svg>

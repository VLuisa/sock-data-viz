<script>
	import { onMount, onDestroy } from 'svelte';
	import { scaleBand, scaleLinear, stack, area, scaleOrdinal } from 'd3';
	import { schemeCategory10 } from 'd3-scale-chromatic';
	import StackedAreaChart from './StackedAreaChart.svelte';

	export let data;
	export let category;
	export let categories;

	$: chartData = data;
</script>

<div>
	<h1>{category}</h1>
	<p>There are {chartData.length} tags in this category</p>
	{#if chartData}
		<StackedAreaChart data={chartData} />
	{/if}
</div>

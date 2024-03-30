<!-- Label.svelte -->
<script>
	export let x;
	export let y;
	export let text;
	export let color;
	export let visible;
</script>

{#if visible}
	<line
		x1={x}
		x2={x + 15}
		y1={y}
		y2={y}
		stroke={color}
	/>

	<text
		x={x + 20}
		y={y}
		text-anchor="start"
		fill="black"
	>
		{text}
	</text>
{/if}

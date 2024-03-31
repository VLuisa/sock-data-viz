<script>
	import { onMount } from 'svelte';

	// @ts-nocheck

	import PositionDisplay from './PositionDisplay.svelte';
	import { csv } from 'd3';

	export let order;
	export let data;

	$: metadata = [];
	$: pattern = data.filter((d) => d.order === order)[0];
	$: img = '';
	$: {
		console.log(img);
	}

	$: {
		if (metadata.length > 0) {
			let currentPattern = metadata.filter((d) => d.meta_order === order)[0];
			img = currentPattern.img_url;
		}
	}

	let permalinkFront = 'https://www.ravelry.com/patterns/library/';

	onMount(async () => {
		metadata = await csv(
			'data/Top 20 patterns - Metadata.csv',
			({ Order, img_url }) => ({
				meta_order: +Order,
				img_url,
			}),
		);
	});
</script>

<div class="pattern-summary">
	<h6>Pattern No. {order}</h6>
	<h1>{pattern.name}</h1>
	<span class="summary-tile"
		>Difficulty average<PositionDisplay
			difficulty={pattern.difficulty}
			outOf="10"
		/></span
	>
	<span class="summary-tile"
		>Rating average<PositionDisplay
			difficulty={pattern.rating}
			outOf="5"
		/></span
	>
	<img
		src={img}
		alt="Current pattern"
	/>
	<a
		href={permalinkFront + pattern.permalink}
		target="_blank">Open in Ravelry</a
	>
</div>

<style>
	.pattern-summary {
		font-family: Helvetica, sans-serif;
		background-color: white;
		margin-top: 20px;
		padding: 10px;
		width: 300px;
		border-radius: 10px;
		border: 1px solid var(--lightgray);
		color: var(--black);
		height: 100%;
	}
	.summary-tile {
		display: flex;
		flex-flow: row nowrap;
		width: 100%;
		justify-content: space-between;
		align-items: center;
		color: var(--darkgray);
	}
	img {
		width: 100%;
		margin-top: 20px;
	}
</style>

<script>
	export let imgurl;
	export let title;
	export let description = '';
	export let altText = '';
	export let footnote = '';
	export let makeWide = false;
</script>

<div class="story">
	{#if title != ''}
		<h2>{title}</h2>
	{/if}
	{#if description != ''}
		<p>{description}</p>
		<div class="spacer-medium" />
	{/if}
</div>
<picture
	style={makeWide
		? 'max-width: 80vw !important; min-width: 78vw !important; align-self: center;'
		: 'min-width: 50vw'}
>
	<img
		src={imgurl}
		alt={altText}
		style="width: 100%; align-self: center;"
	/>
</picture>
<div class="story">
	{#if footnote != ''}
		<!-- <div class="spacer-small" /> -->
		<p class="footnote"><strong>Note: </strong>{footnote}</p>
	{/if}
</div>

<style>
	img {
		width: 100%;
		justify-self: center;
		margin-bottom: 5vh;
		align-self: center;
	}
</style>

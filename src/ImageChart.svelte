<script>
	export let imgurl;
	export let title;
	export let description = '';
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
<picture style={makeWide ? 'max-width: 80vw !important' : 'min-width: 50vw'}>
	<!-- <source srcset="img_smallflower.jpg" media="(max-width: 600px)">
        <source srcset="img_flowers.jpg" media="(max-width: 1500px)">
        <source srcset="flowers.jpg"> -->
	<img
		src={imgurl}
		alt={description}
		style="width: 100%;"
	/>
</picture>
<div class="story">
	{#if footnote != ''}
		<div class="spacer-medium" />
		<p class="footnote"><strong>Note: </strong>{footnote}</p>
	{/if}
	<!-- <object
		type="image/svg+xml"
		data="img/HeelDifficulty.svg"
	></object> -->
</div>

<style>
	/* div {
		max-width: 900px;
	} */
	img {
		max-width: 100%;
		justify-self: center;
		margin-bottom: 5vh;
	}
</style>

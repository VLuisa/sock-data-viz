<script>
	export let imgurl;
	export let title;
	export let description = '';
	export let footnote = '';
	export let makeWide = false;
</script>

<div class="story">
	<h2>{title}</h2>
	{#if description != ''}
		<p>{description}</p>
	{/if}
	<div class="spacer-medium" />
</div>
<picture style={makeWide ? 'max-width: 80vw !important' : 'max-width: 50vw'}>
	<!-- <source srcset="img_smallflower.jpg" media="(max-width: 600px)">
        <source srcset="img_flowers.jpg" media="(max-width: 1500px)">
        <source srcset="flowers.jpg"> -->
	<img
		src={imgurl}
		alt="Dot plot showing that heel tags are not the most difficult"
		style="width:auto;"
	/>
</picture>
<div class="story">
	<div class="spacer-medium" />
	{#if footnote != ''}
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
	}
</style>

<script>
	export let category;
	export let width;

	const imagePath = '/img/';

	const images = {
		Heel: 'heel',
		Toe: 'toe',
		Colorwork: 'colorwork',
		'Fabric / Stitches': 'fabric',
		'Sock Method': 'method',
	};
</script>

<img
	src={imagePath + images[category] + '.png'}
	alt={category}
	style="width:{width}px"
/>

<style>
	img {
		/* width: 150px; */
		height: 100%;
		margin-top: 100px;
		transition: opacity 0.3s ease-out;
		margin-right: -50px;
		z-index: 5;
	}
</style>

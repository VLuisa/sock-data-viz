<script>
	export let type = 'section';
</script>

<div>
	{#if type === 'section'}
		<img
			src="img/decorative-swirl.png"
			class="section"
			alt="decorative handdrawn swirl"
		/>
	{:else if type === 'subsection'}
		<img
			src="img/decorative-swirl-small.png"
			class="subsection"
			alt="small decorative handdrawn swirl"
		/>
	{/if}
</div>

<style>
	div {
		display: flex;
		justify-content: center;
	}
	.section {
		margin-top: 50px;
		margin-bottom: 50px;
		width: 100px;
		height: auto;
	}

	.subsection {
		margin-top: 15px;
		margin-bottom: 25px;
		width: 60px;
		height: auto;
	}
</style>

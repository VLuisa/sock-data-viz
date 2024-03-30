<script>
	export let categories;
	export let setActiveCategory;

	function handleClick(category) {
		setActiveCategory(category);
	}
</script>

<div class="filter-buttons">
	{#each categories as category}
		<button on:click={() => handleClick(category)}>{category}</button>
	{/each}
</div>

<style>
	.filter-buttons {
		display: flex;
		gap: 10px;
	}
</style>

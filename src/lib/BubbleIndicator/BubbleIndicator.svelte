<script>
	export let count;
	export let selected; //for binding
	import DiashowIndicatorBubble from './BubbleIndicatorBubble.svelte';
</script>

<div class="diashowIndicatorContainer">
	{#each [...Array(count).keys()] as i}
		<div
			class="diashowIndicatorBubble"
		>
			<DiashowIndicatorBubble selected={i === selected} />
		</div>
	{/each}
</div>

<style>
	.diashowIndicatorContainer {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
	}
</style>

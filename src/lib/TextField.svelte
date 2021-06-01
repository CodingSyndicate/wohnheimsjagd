<script>
	export let value;
	export let invalid = false;
</script>

<input class:invalid bind:value placeholder="Your answer..." on:change={() => {invalid = false;}}/>

<style>
	input {
		height: 50px;
		width: 80%;
		margin: 0.5rem;
	}
	.invalid{
		border: 1px solid red;
	}
</style>

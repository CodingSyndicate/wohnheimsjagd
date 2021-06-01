<script>
	import Button from '$lib/Button.svelte';
	import TextField from '$lib/TextField.svelte';
	import { data } from '$lib/data';
	import BubbleIndicator from '$lib/BubbleIndicator/BubbleIndicator.svelte';

	let currentAnswer = '';

	let currentStation = 0;
	let languageCode = 0;

	function checkAnswer(answers, answer) {
		if (answers.includes(answer)) {
			console.log('Yeah');
			currentStation++;
			currentAnswer = '';
		} else {
			console.log('Wrong!');
		}
	}
</script>

<div class="indexContainer">
	<h1 class="title">Schnitzeljagd</h1>
	<p class="info">
		VORSICHT! Ihr begebt euch auf gefährliches Teritorium! Die Wege vor euch werden von der
		Pinguinguerillia kontrolliert!
		<br />
		<br />
		Um die Pinguine friedlich zu gesinnen, müsst ihr nun klein Pingu bei seinen Hausaufgaben helfen,
		damit er für euch bei den Kaiserpinguinen bürgt.
	</p>

	<h3 class="pinguTitle">Pingus Hausaufgaben:</h3>
	{#each [data[currentStation]] as station (currentStation)}
		<p class="stationHint">{station.hint[languageCode]}</p>
		{#if station.question}
			<p class="stationQuestion">{station.question[languageCode]}</p>
			<TextField bind:value={currentAnswer} />
			<Button on:click={checkAnswer(station.answers, currentAnswer.toLowerCase())} />
		{:else}
			Pinguine können nicht fliegen. Dafür sind sie sehr gute Schwimmer und Taucher.
		{/if}
	{/each}
	<BubbleIndicator count={data.length} bind:selected={currentStation} />
</div>

<style>
	.indexContainer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding-left: 2rem;
		padding-right: 2rem;
	}

	.stationHint {
		font-style: italic;
	}
	.stationQuestion {
		margin-bottom: 0;
	}
</style>

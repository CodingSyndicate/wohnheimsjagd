<script>
	import Button from '$lib/Button.svelte';
	import TextField from '$lib/TextField.svelte';
	import { data } from '$lib/data';
	import BubbleIndicator from '$lib/BubbleIndicator/BubbleIndicator.svelte';

	let currentAnswer = '';

	let currentStation = 0;
	let languageCode = 0;
	let invalid = false;

	function checkAnswer(answers, answer) {
		gtag('event', data[currentStation].name, {
			value: answer
		});

		if (answers.includes(answer)) {
			console.log('Correct answer!');
			currentStation++;
			currentAnswer = '';
		} else {
			invalid = true;
			console.log('Wrong answer :(');
		}
	}

	function changeLanguage(code) {
		languageCode = code;
		gtag('event', 'language', {
			value: languageCode === 0 ? 'deutsch' : 'englisch'
		});
	}
</script>

<div class="indexContainer">
	<div class="titleRow">
		<div class="corner" />
		<h1 class="title">Schnitzeljagd</h1>
		<div class="languageSelection corner">
			<img class="language" src="/deutschland.jpg" alt="" on:click={changeLanguage(0)} />
			<img class="language" src="/britanien.png" alt="" on:click={changeLanguage(1)} />
		</div>
	</div>
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
			<TextField bind:value={currentAnswer} bind:invalid />
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

	.titleRow {
		width: 100%;
		display: flex;
		flex-direction: row;
		justify-content: space-evenly;
		align-items: center;
	}

	.language {
		padding: 0.25rem;
		width: 30px;
		height: 25px;
	}

	.title {
		width: 80%;
		text-align: center;
	}

	.corner {
		width: 10%;
	}

	.stationHint {
		font-style: italic;
	}
	.stationQuestion {
		margin-bottom: 0;
	}
</style>

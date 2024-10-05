<script lang="ts">
	import { score } from '$lib/store';
	import ClickField from './clickField.svelte';

	let score_value: number;
	let gameStarted = false;

	score.subscribe((value) => {
		score_value = value;
	});

	const startGame = () => {
		gameStarted = true;
	};
</script>

<div>
	<h1>clicking</h1>
	<p>
		get the circles and ignore the squares. score: {score_value}
	</p>
	<button on:click={startGame}> start </button>
	{#if gameStarted}
		<ClickField />
	{/if}
</div>

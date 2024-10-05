<script lang="ts">
	import { ShapeType } from '$lib';
	import { score } from '$lib/store';
	import { onMount } from 'svelte';
	import Circle from './circle.svelte';
	import Square from './square.svelte';

	export let type: ShapeType;
	export let position: { x: number; y: number };
	export let onRemove;
	const timeout = 1000;

	const scoreUp = () => {
		score.update((n) => n + 1);
	};

	const scoreDown = () => {
		score.update((n) => n - 1);
	};

	const clicked = () => {
		if (type === ShapeType.CIRCLE) {
			scoreUp();
		}

		if (type === ShapeType.SQUARE) {
			scoreDown();
		}

		onRemove();
	};

	onMount(() => {
		setTimeout(onRemove, timeout);
	});
</script>

<button class="shape" on:click={clicked} style:top="{position.x}px" style:left="{position.y}px">
	{#if type === ShapeType.CIRCLE}
		<Circle />
	{:else if type === ShapeType.SQUARE}
		<Square />
	{/if}
</button>

<style>
	.shape {
		all: unset;
		display: inline-block;
		cursor: pointer;
		position: absolute;
	}
</style>

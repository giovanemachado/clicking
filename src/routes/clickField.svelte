<script lang="ts">
	import { ShapeType } from '$lib';
	import Shape from './shape.svelte';
	import { onMount } from 'svelte';

	let shapes: {
		id: number;
		type: ShapeType;
		x: number;
		y: number;
	}[] = [];
	let shapeCounter = 0;
	let timeout = 1000;
	let containerWidth = 800;
	let containerHeight = 800;

	const getRandomPosition = () => {
		const x = Math.floor(Math.random() * (containerWidth - 100));
		const y = Math.floor(Math.random() * (containerHeight - 100));
		return { x, y };
	};

	const createShape = () => {
		const position = getRandomPosition();
		const isCircle = Math.random() < 0.5;

		shapes = [
			...shapes,
			{
				id: shapeCounter,
				type: isCircle ? ShapeType.CIRCLE : ShapeType.SQUARE,
				x: position.x,
				y: position.y
			}
		];

		shapeCounter++;
	};

	const removeShape = (id: number) => {
		shapes = shapes.filter((shape) => shape.id !== id);
	};

	onMount(() => {
		setInterval(createShape, timeout);
	});
</script>

<div class="container">
	{#each shapes as shape}
		<Shape
			onRemove={() => removeShape(shape.id)}
			type={shape.type}
			position={{ x: shape.x, y: shape.y }}
		/>
	{/each}
</div>

<style>
	.container {
		width: 800px;
		height: 800px;
		border: black;
		border-width: 1px;
		border-style: solid;
		position: relative;
		overflow: hidden;
		margin-top: 5px;
	}
</style>

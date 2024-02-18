<script lang="ts">
	import { onMount } from 'svelte';

	let canvas: HTMLCanvasElement;
	let ctx: CanvasRenderingContext2D;
	let padding: number = 20;

	onMount(() => {
		canvas.width = 800 + padding * 2;
		canvas.height = 600 + padding * 2;
		ctx = canvas.getContext('2d')!;
		drawBreadboard();
		canvas.addEventListener('click', handleClick);
	});
	let gapX: number;
	let gapY: number;
	let holeRadius: number = 5;

	function drawBreadboard() {
		const width: number = canvas.width - padding * 2;
		const height: number = canvas.height - padding * 2;

		// Set background color
		ctx.fillStyle = '#f0f0f0';
		ctx.fillRect(padding, padding, width, height);

		// Draw holes
		const rows: number = 10;
		const cols: number = 30;
		gapX = (width - holeRadius * 2) / (cols - 1);
		gapY = (height - holeRadius * 2) / (rows - 1);

		ctx.fillStyle = '#000';
		for (let row = 0; row < rows; row++) {
			for (let col = 0; col < cols; col++) {
				const x: number = padding + holeRadius + col * gapX;
				const y: number = padding + holeRadius + row * gapY;
				ctx.beginPath();
				ctx.arc(x, y, holeRadius, 0, 2 * Math.PI);
				ctx.fill();
			}
		}
	}

	function handleClick(event: MouseEvent) {
		const x = event.clientX - canvas.offsetLeft - padding;
		const y = event.clientY - canvas.offsetTop - padding;

		const dotX = Math.round((x - holeRadius) / gapX);
		const dotY = Math.round((y - holeRadius) / gapY);

		console.log(`Dot at (${dotX}, ${dotY}) was clicked`);
	}
</script>

<canvas id="board" bind:this={canvas}></canvas>

<style>
	#board {
		margin: auto;
		display: block;
		border: 1px solid #ccc;
		background-color: #f0f0f0;
	}
</style>

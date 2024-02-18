<script lang="ts">
	import { onMount } from 'svelte';

	let canvas: HTMLCanvasElement;
	let ctx: CanvasRenderingContext2D;
	let padding: number = 20;

	onMount(() => {
		canvas.width = window.innerWidth - padding;
		canvas.height = window.innerHeight - padding;
		ctx = canvas.getContext('2d')!;
		drawBreadboard();
	});

	function drawBreadboard() {
		const width: number = canvas.width;
		const height: number = canvas.height;

		// Set background color
		ctx.fillStyle = '#f0f0f0';
		ctx.fillRect(0, 0, width, height);

		// Draw holes
		const rows: number = 10; // Adjust based on your breadboard size
		const cols: number = 30; // Adjust based on your breadboard size
		const holeRadius: number = 3;
		const gap: number = 10;

		ctx.fillStyle = '#000';
		for (let row = 0; row < rows; row++) {
			for (let col = 0; col < cols; col++) {
				const x: number = gap + col * (2 * holeRadius + gap);
				const y: number = gap + row * (2 * holeRadius + gap);
				ctx.beginPath();
				ctx.arc(x, y, holeRadius, 0, 2 * Math.PI);
				ctx.fill();
			}
		}
	}
</script>

<canvas bind:this={canvas} width="300" height="200"></canvas>

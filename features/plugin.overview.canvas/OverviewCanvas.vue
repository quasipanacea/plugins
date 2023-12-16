<template>
	<canvas class="canvas"></canvas>
</template>

<script setup lang="ts">
import { onMounted } from 'vue'

let canvas: HTMLCanvasElement | null
let ctx: CanvasRenderingContext2D | null

onMounted(async () => {
	canvas = document.querySelector('canvas')
	if (!canvas) {
		throw new Error("Failed to get canvas element")
	}

	ctx = canvas?.getContext('2d')
	if (!ctx) {
		throw new Error("Failed to get 2d canvas context");
	}
})

onMounted(() => {
	draw();
})
document.addEventListener('resize', () => {
	draw();
})

function drawDot(ctx: CanvasRenderingContext2D, x: number, y: number) {
	let radius = 5

	ctx.beginPath();
	ctx.arc(x, y, radius, 0, 2 * Math.PI, false);
	ctx.fillStyle = '#868e96';
	ctx.fill();
}

function drawDots(ctx: CanvasRenderingContext2D, startX: number, startY: number) {
	let radius = 5
	let spacing = 20

	for (let h = 0; h < 20; ++h) {
		for (let v = 0; v < 5; ++v) {
			let x = startX + (h * spacing);
			let y = startY + (v * spacing);
			drawDot(ctx, x, y);
		}
	}

}

function draw() {
	if (!canvas) return
	if (!ctx) return;

	let x = canvas.parentNode?.getBoundingClientRect().width
	let y = canvas.parentNode?.getBoundingClientRect().height
	canvas.setAttribute('width', x - 2)
	canvas.setAttribute('height', y - 3)

	ctx.fillRect(25, 25, 50, 50)

	drawDot(ctx, 500, 20);
	drawDots(ctx, 20, 20)
}
</script>

<style scoped>
.canvas {
	border: 1px solid darksalmon;
}
</style>

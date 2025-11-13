<script lang="ts">
	import { onMount } from 'svelte';

	// This component creates a starry background using CSS and JavaScript.
	// It dynamically generates star elements and positions them randomly within the container.
	// Each star has a random size, opacity, and animation duration to create a twinkling effect.
	onMount(() => {
		const starsContainer = document.querySelector('.stars') as HTMLElement | null;
		if (!starsContainer) return;

		const numStars = 120; // Number of stars to create
		for (let i = 0; i < numStars; i++) {
			const star = document.createElement('div');
			star.classList.add('star');
			star.style.top = `${Math.random() * 100}%`;
			star.style.left = `${Math.random() * 100}%`;
			star.style.animationDuration = `${2 + Math.random() * 3}s`;
			star.style.animationDelay = `${Math.random() * 5}s`;
			star.style.opacity = (0.1 + Math.random() * 0.3).toFixed(2);
			star.style.transform = `scale(${0.5 + Math.random() * 1.5})`;
			starsContainer.appendChild(star);
		}
	});
</script>

<div class="stars" aria-hidden="true"></div>

<style>
	.stars {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		pointer-events: none;

		:global(.star) {
			position: absolute;
			width: 2px;
			height: 2px;
			background: white;
			border-radius: 50%;
			opacity: 0.2;
			animation: twinkle 5s infinite ease-in-out;
		}
	}

	@keyframes twinkle {
		0%,
		100% {
			opacity: 0.15;
			transform: scale(1);
		}
		50% {
			opacity: 0.4;
			transform: scale(1.5);
		}
	}
</style>

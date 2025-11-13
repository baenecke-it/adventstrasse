<script lang="ts">
	import '$lib/css/global.scss';
	import favicon from '$lib/assets/favicon.png';
	import Footer from '$lib/components/Footer.svelte';
	import Stars from '$lib/components/Stars.svelte';
	import Roofs from '$lib/components/Roofs.svelte';
	import Snow from '$lib/components/Snow.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<main id="main">
	<Stars></Stars>
	<Snow></Snow>
	<Roofs></Roofs>
	{@render children()}
</main>
<Footer />

<style>
	:root {
		--bg-top: #182033;
		--bg-bottom: #05060a;
		--card-bg: rgba(0, 0, 0, 0.45);
		--accent: rgba(255, 225, 140, 0.95);
		--color: #ffffff; /* TODO: use for text-color */
		--muted: #6b7280; /* TODO: use for all muted text */
		--footer-height: 40px;
	}

	#main {
		color: #fff;
		height: 100lvh;
		background: radial-gradient(ellipse at bottom, var(--bg-top) 0%, var(--bg-bottom) 100%);
		position: relative;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 0 0 var(--footer-height);
	}
</style>

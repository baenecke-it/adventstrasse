<script lang="ts">
	import coverImage from '$lib/assets/cover_adventstrasse.jpg';
	import backCoverImage from '$lib/assets/backcover_adventstrasse.jpg';
	import spineImage from '$lib/assets/spine_adventstrasse.jpg';
	import PurchaseSection from '$lib/components/sections/PurchaseSection.svelte';
	import Stars from '$lib/components/Stars.svelte';
	import Snow from '$lib/components/Snow.svelte';
	import Roofs from '$lib/components/Roofs.svelte';
</script>

<svelte:head>
	<title>Adventstraße – Der Düsterweg erwacht</title>
</svelte:head>

<Stars></Stars>
<Snow></Snow>
<Roofs></Roofs>
<PurchaseSection
	book={{
		title: 'Die Adventstraße',
		author: 'Dorothea Schaller',
		coverImage: coverImage,
		spineImage: spineImage,
		backCoverImage: backCoverImage,
		priceHardcover: '15,99 €',
		priceSoftcover: '9,99 €',
		amazonUrl: 'https://amzn.eu/d/ePQiZNm',
		email: 'adventstrasse@mail.de'
	}}
></PurchaseSection>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600&family=Lato:wght@400;700&display=swap');

	:root {
		--bg-top: #182033;
		--bg-bottom: #05060a;
		--card-bg: rgba(0, 0, 0, 0.45);
		--accent: rgba(255, 225, 140, 0.95);
		--footer-height: 60px;
		--footer-height-mobile: 80px;
	}

	:global(html),
	:global(body) {
		height: 100vh;
		overflow: hidden;
	}

	:global(body) {
		font-family: 'Lato', sans-serif;
		color: #fff;
		height: 100dvh;
		background: radial-gradient(ellipse at bottom, var(--bg-top) 0%, var(--bg-bottom) 100%);
		position: relative;
		text-align: center;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 2rem;
		padding-bottom: calc(2rem + var(--footer-height));
	}

	@media screen and (max-width: 720px) {
		:global(body) {
			padding-bottom: calc(2rem + var(--footer-height-mobile));
		}
	}
</style>

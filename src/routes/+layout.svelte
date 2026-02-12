<script lang="ts">
    import '$lib/css/global.scss';
    import Footer from '$lib/components/Footer.svelte';
    import Stars from "$lib/components/Stars.svelte";
    import Roofs from "$lib/components/Roofs.svelte";
    import Snow from "$lib/components/Snow.svelte";

    let { children } = $props();
</script>

<svelte:head>
    <link rel="icon" type="image/png" href="/favicon-96x96.png" sizes="96x96" />
    <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
    <link rel="shortcut icon" href="/favicon.ico" />
    <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png" />
    <meta name="apple-mobile-web-app-title" content="Adventstraße" />
    <link rel="manifest" href="/site.webmanifest" />
</svelte:head>

<a href="#main-content" class="skip-to-content">Zum Hauptinhalt springen</a>

<main id="main">
    <Stars></Stars>
    <Snow></Snow>
    <Roofs></Roofs>
    <div id="main-content">
        {@render children()}
    </div>
</main>
<Footer/>

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
        min-height: 100dvh;
        background: radial-gradient(ellipse at bottom, var(--bg-top) 0%, var(--bg-bottom) 100%);
        position: relative;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        padding: 0 0 var(--footer-height);
    }
</style>
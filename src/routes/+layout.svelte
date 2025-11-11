<script lang="ts">
    import '$lib/css/global.scss';
    import favicon from '$lib/assets/favicon.png';
    import Footer from '$lib/components/Footer.svelte';
    import Stars from "$lib/components/Stars.svelte";
    import Roofs from "$lib/components/Roofs.svelte";
    import Snow from "$lib/components/Snow.svelte";

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
<Footer/>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600&family=Lato:wght@400;700&display=swap');

    :root {
        --bg-top: #182033;
        --bg-bottom: #05060a;
        --card-bg: rgba(0, 0, 0, 0.45);
        --accent: rgba(255, 225, 140, 0.95);
        --footer-height: 60px;
        --footer-height-mobile: 70px;
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
        padding: 2rem 2rem calc(2rem + var(--footer-height));
    }

    @media screen and (max-width: 720px) {
        #main {
            padding-bottom: calc(2rem + var(--footer-height-mobile));
        }
    }
</style>
<script lang="ts">
    import '$lib/css/global.scss';
    import favicon from '$lib/assets/favicon.png';
    import Footer from '$lib/components/Footer.svelte';

    let { children } = $props();
</script>

<svelte:head>
    <link rel="icon" href={favicon} />
</svelte:head>

{@render children()}

<Footer />

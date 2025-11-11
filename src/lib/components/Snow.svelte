<script lang="ts">
    import {onMount} from "svelte";

    // This component creates a snowfall effect using CSS and JavaScript.
    // It dynamically generates snowflake elements and positions them randomly within the container.
    // Each snowflake has a random size, opacity, and animation duration to create a natural falling effect.
    onMount(() => {
        const snowContainer = document.querySelector('.snow') as HTMLElement | null;
        if (!snowContainer) return;

        const numFlakes = 60; // Number of snowflakes to create
        for (let i = 0; i < numFlakes; i++) {
            const flake = document.createElement('div');
            flake.classList.add('flake');
            flake.textContent = '❄';
            flake.style.fontSize = (0.2 + Math.random() * 0.5) + 'rem';
            flake.style.left = `${Math.random() * 100}%`;
            flake.style.opacity = (0.2 + Math.random() * 0.5).toFixed(2);
            flake.style.animationDuration = `${3 + Math.random() * 5}s`;
            // flake.style.animationDuration = (10 + Math.random()*10) + 's';
            flake.style.animationDelay = `${Math.random() * 10}s`;
            snowContainer.appendChild(flake);
        }
    });
</script>

<div class="snow" aria-hidden="true"></div>

<style>
    .snow {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        pointer-events: none;
        z-index: 0;

        :global(.flake) {
            position: absolute;
            top: -10%;

            color: white;
            font-size: 0.3rem;
            user-select: none;
            pointer-events: none;
            opacity: 0.8;
            animation: fall linear infinite;
        }
    }

    /* Feiner Schneefall mit Windbewegung */
    @keyframes fall {
        0% {
            transform: translateY(-10vh) translateX(0vw);
            opacity: 0.8;
        }
        100% {
            transform: translateY(110vh) translateX(20px); /* 30px */
            opacity: 0.2;
        }
    }

    /* Schneefall mit leichtem Wind */
    /*@keyframes fall {*/
    /*    0% {transform: translate3d(0, 0, 0) rotate(0deg); opacity: 0.9;}*/
    /*    50% {transform: translate3d(10vw, 50vh, 0) rotate(180deg); opacity: 0.7;}*/
    /*    100% {transform: translate3d(-5vw, 100vh, 0) rotate(360deg); opacity: 0.3;}*/
    /*}*/
</style>
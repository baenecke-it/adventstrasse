<script lang="ts">
    import {onMount} from "svelte";

    onMount(() => {

    });
</script>

<div class="window" aria-hidden="true"></div>
<div class="roofs" aria-hidden="true"></div>

<style>
    .roofs {
        position: fixed;
        bottom: 0;
        width: 100%;
        height: 42vh;
        background: linear-gradient(to top, #232733 0%, #3c4150 40%, transparent 100%);
        clip-path: polygon(0% 100%, 5% 85%, 15% 95%, 25% 80%, 40% 100%, 55% 85%, 65% 95%, 80% 70%, 100% 100%);
        z-index: 2;
        filter: drop-shadow(0 -8px 18px rgba(0, 0, 0, 0.6));
        pointer-events: none;
    }

    .roofs::before {
        content: "";
        position: absolute;
        inset: 0;
        background: linear-gradient(to top, rgba(255, 255, 255, 0.28) 6%, transparent 70%);
        clip-path: inherit;
        opacity: 0.7;
    }

    .window {
        position: fixed;
        z-index: 3;
        width: 56px;
        height: 56px;
        bottom: 22vh;
        right: 9%;
        border-radius: 6px;
        background: linear-gradient(180deg, #fff3c0 0%, #ffdd88 40%, #ffdf9f 100%);
        box-shadow: 0 0 28px 8px rgba(255, 220, 120, 0.12), inset 0 -6px 12px rgba(0, 0, 0, 0.06);
        display: flex;
        align-items: center;
        justify-content: center;
        transform: rotate(-6deg);
        animation: flicker 3s infinite;
        border: 1px solid rgba(0, 0, 0, 0.12);
        pointer-events: none;
    }

    .window::before {
        content: "";
        position: absolute;
        inset: 8px;
        border-radius: 4px;
        box-shadow: inset 0 0 0 2px rgba(0, 0, 0, 0.12);
    }

    .window::after {
        content: "";
        position: absolute;
        width: 68%;
        height: 68%;
        border-left: 2px solid rgba(0, 0, 0, 0.12);
        border-top: 2px solid rgba(0, 0, 0, 0.12);
        transform: translateY(-4%);
    }

    @keyframes flicker {
        0% {
            filter: brightness(1.06)
        }
        10% {
            filter: brightness(0.95)
        }
        25% {
            filter: brightness(1.12)
        }
        45% {
            filter: brightness(0.98)
        }
        70% {
            filter: brightness(1.08)
        }
        100% {
            filter: brightness(1.02)
        }
    }

    @media (max-width: 720px) {
        .window {
            width: 44px;
            height: 44px;
            bottom: 18vh;
            right: 6%
        }
    }
</style>
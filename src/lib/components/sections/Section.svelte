<script lang="ts">
    export let right: boolean | null = false;
    export let id = '';
    export let anchor = '.5';
    export let offsetX = '75%';
    export let rotation = -30;
    export let scale = 1;
</script>

<section id="{id}" class="scroll-section {right === null ? 'full' : (right ? 'right' : '')}" data-anchor="{anchor}" data-offset-x="{offsetX}" data-rotation="{rotation}" data-scale={scale}>
    <div class="container">
        <slot></slot>
    </div>
</section>

<style>
    .scroll-section {
        position: relative;
        height: 100vh;
        width: 100vw;
        overflow: hidden;
        display: flex;
        align-items: center;
        justify-content: flex-start;

        &.right {
            justify-content: flex-end;
        }

        .container {
            position: relative;
            width: 50%;
            height: 100%;
        }

        &.full .container {
            width: 100%;
        }
    }
</style>
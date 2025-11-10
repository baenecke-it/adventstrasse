<script>
    export let right = false;
    export let id = '';
    export let anchor = '.5';
    export let offsetX = '75%';
    export let rotation = -30;
</script>

<section id="{id}" class="scroll-section {right ? 'right' : ''}" data-anchor="{anchor}" data-offset-x="{offsetX}" data-rotation="{rotation}">
    <div class="container">
        <slot></slot>
    </div>
</section>

<style>
    .scroll-section {
        position: absolute;
        height: 100vh;
        width: 50vw;
        overflow: hidden;
        display: flex;
        align-items: center;

        &:not(:first-of-type) {
            width: 0;
        }

        .container {
            position: absolute;
            width: 50vw;
            height: 100%;
        }

        &.right {
            right: 0;
            .container {
                right: 0;
            }
        }

        @media (max-width: 768px) {
            position: relative;
            width: 100% !important;
            height: auto;
            top: 0;
            .container {
                position: relative;
                width: 100%;
            }
        }
    }
</style>
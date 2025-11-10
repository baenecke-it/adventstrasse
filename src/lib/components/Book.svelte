<script lang="ts">
    export let coverImage: string = '';
    export let coverImageAlt: string = 'Book Cover';

    export let spineImage: string = '';
    export let spineImageAlt: string = 'Book Spine';
    export let spineDir: boolean = true; // true = top to bottom, false = bottom to top

    export let backCoverImage: string = '';
    export let backCoverImageAlt: string = 'Back Cover';

    export let width: number = 200;
    export let height: number = 300;
    export let depth: number = 30;
    export let unit: string = 'px';
    export let scale: number = 1;

    export let shadow: boolean = true;
    export let coverColor: string = '#4f46e5';
    export let pageColor: string = '#f8f7f3';

    export let initialRotation: number = -30;
    export let transition: boolean = true;

    export function setRotation(deg: number) {
        const book = document.querySelector<HTMLElement>('.book');
        if (book) {
            book.style.transform = `rotateY(${deg}deg)`;
        }
    }
</script>

<style>
    .book-container {
        display: flex;
        align-items: center;
        justify-content: center;
        perspective: 600px;
    }

    @keyframes initAnimation {
        5% {
            visibility: hidden;
            transform: rotateY(0deg);
        }
        100% {
            visibility: visible;
            transform: rotateY(var(--initial-rotation, -30deg));
        }
    }

    .book {
        width: 100%; /*TODO: 90%, but then pages offset und so muss angepasst werden */
        height: 100%;
        position: relative;
        transform-style: preserve-3d;
        transform: rotateY(var(--initial-rotation, -30deg));
        transition: var(--transition);
        /*animation: 1s ease 0s 1 initAnimation;*/

        .book-container:hover &,
        .book-container:focus & {
            transform: rotateY(0deg);
        }

        /* Front and Back Covers */
        .cover {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: var(--cover-color);
            border-radius: 0 2px 2px 0;
            box-shadow: 5px 5px 20px #666;

            &.front {
                transform: translateZ(var(--cover-offset));
            }

            &.back {
                transform: translateZ(var(--backcover-offset)) rotateY(180deg);
                background-color: var(--cover-color);
                box-shadow: var(--book-shadow, none);
            }

            &.text {
                display: flex;
                align-items: center;
                justify-content: center;
                color: white;
                font-weight: bold;
                text-align: center;
            }
        }
    }

    /* Spine */
    .spine {
        position: absolute;
        top: 0;
        left: 0;
        width: var(--depth);
        height: 100%;
        background-color: var(--cover-color);
        transform: translateX(var(--spine-offset)) rotateY(-90deg);
        border-radius: 0 2px 2px 0;

        &.text {
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            text-align: center;
            writing-mode: var(--spine-writing-mode);
        }
    }

    /* Pages */
    .book::before {
        position: absolute;
        content: ' ';
        left: 0;
        top: 1px;
        width: calc(var(--depth) - var(--pages-delta));
        height: calc(var(--height) - var(--pages-delta));
        transform: translateX(var(--pages-offset)) rotateY(90deg);
        background: blue linear-gradient(90deg,
        #fff 0%,
        #f9f9f9 5%,
        #fff 10%,
        #f9f9f9 15%,
        #fff 20%,
        #f9f9f9 25%,
        #fff 30%,
        #f9f9f9 35%,
        #fff 40%,
        #f9f9f9 45%,
        #fff 50%,
        #f9f9f9 55%,
        #fff 60%,
        #f9f9f9 65%,
        #fff 70%,
        #f9f9f9 75%,
        #fff 80%,
        #f9f9f9 85%,
        #fff 90%,
        #f9f9f9 95%,
        #fff 100%
        );
    }
</style>

<a
        class="book-container"
        href="#buy"
        target="_blank"
        rel="noreferrer noopener"
        style="--cover-color: {coverColor};
                --book-shadow: {shadow ? '-10px 0 50px 10px #666' : 'none'};
                --spine-writing-mode: {spineDir ? 'sideways-rl' : 'sideways-lr'};
                --depth: {depth * scale}{unit};
                --cover-offset: {depth * scale / 2}{unit};
                --backcover-offset: -{depth * scale / 2}{unit};
                --spine-offset: -{depth * scale / 2}{unit};
                --height: {height * scale}{unit};
                --pages-delta: {2 * scale}{unit};
                --pages-offset: {(width * scale) - (depth * scale / 2) - scale}{unit};
                --initial-rotation: {initialRotation}deg;
                --transition: {transition ? 'transform 0.5s ease' : 'none'};
               width: {width * scale}{unit};
               height: {height * scale}{unit};"
>
    <div class="book">
        {#if coverImage}
            <img class="cover front"
                 alt="{coverImageAlt}"
                 src="{coverImage}"
            />
        {:else}
            <div class="cover front text"
            >{coverImageAlt}
            </div>
        {/if}
        {#if spineImage}
            <img class="spine"
                 alt="{spineImageAlt}"
                 src="{spineImage}"
            />
        {:else}
            <div class="spine text"
            >{spineImageAlt}
            </div>
        {/if}
        {#if backCoverImage}
            <img class="cover back"
                 alt="{backCoverImageAlt}"
                 src="{backCoverImage}"
            />
        {:else}
            <div class="cover back text"
            >{backCoverImageAlt}
            </div>
        {/if}
    </div>
</a>
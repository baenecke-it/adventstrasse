<script lang="ts">
    import {onMount} from 'svelte';
    import Book from '../Book.svelte';
    import AmazonLogo from '$lib/assets/icons/amazon.svelte';
    import MailIcon from '$lib/assets/icons/at-sign.svelte';

    interface BookData {
        title: string;
        author?: string;
        coverImage?: string;
        spineImage?: string;
        backCoverImage?: string;
        priceHardcover?: string;
        priceSoftcover?: string;
        amazonUrl?: string;
        email?: string;
    }

    export let book: BookData = {
        title: 'Beispielbuch',
        author: 'Max Mustermann',
        coverImage: '', // optional: Pfad zur Cover‑Bilddatei
        spineImage: '', // optional: Pfad zur Buchrücken‑Bilddatei
        backCoverImage: '', // optional: Pfad zur Rückseiten‑Bilddatei
        priceHardcover: '__,__ €',
        priceSoftcover: '__,__ €',
    };

    let bookRef: Book;

    onMount(() => {
        const purchaseSection = document.querySelector<HTMLElement>('.purchase-section');
        const bookWrapper = purchaseSection?.querySelector<HTMLElement>('[role="button"]');
        const bookEl = bookWrapper?.querySelector<HTMLElement>('.book');
        if (!purchaseSection || !bookEl || !bookWrapper) return;

        function clamp(num: number, min: number, max: number): number {
            return Math.min(Math.max(num, min), max);
        }

        let front = true;
        let isTouching = false;
        const defaultRotation = -30; // Default slightly angled position

        const onPointerMove = (event: MouseEvent | TouchEvent) => {
            if (!bookRef) return;

            let pointerData: MouseEvent | Touch;
            const isTouch = event instanceof TouchEvent;

            if (isTouch) {
                if (event.touches.length > 0) {
                    pointerData = event.touches[0];
                } else {
                    return;
                }
            } else {
                pointerData = event;
            }

            const rect = bookEl.getBoundingClientRect();
            const centerX = rect.left + rect.width / 2;
            const centerY = rect.top + rect.height / 2;

            const deltaX = pointerData.clientX - centerX;
            const deltaY = pointerData.clientY - centerY;

            const rotateY = clamp((deltaX / (rect.width / 2)) * 30, -40, 40); // Max +-40 degrees
            const rotateX = clamp((-deltaY / (rect.height / 2)) * 10, -15, 15); // Max +-15 degrees

            requestAnimationFrame(() => {
                // Enable transition for touch on mobile
                bookRef.setRotation(rotateY + (front ? 0 : 180), rotateX * (front ? 1 : -1), 0, isTouch);
            });
        }

        // Handle touchstart to rotate book to finger immediately
        const onTouchStart = (event: TouchEvent) => {
            if (!bookRef) return;
            isTouching = true;
            onPointerMove(event);
        };

        // Reset book rotation when touch ends (finger lifted)
        const onTouchEnd = () => {
            if (!bookRef) return;
            isTouching = false;
            requestAnimationFrame(() => {
                bookRef.setRotation(front ? defaultRotation : 180 + defaultRotation, 0, 0, true);
            });
        };

        window.addEventListener('mousemove', onPointerMove);
        purchaseSection.addEventListener('touchstart', onTouchStart, { passive: true });
        purchaseSection.addEventListener('touchmove', onPointerMove, { passive: true });
        purchaseSection.addEventListener('touchend', onTouchEnd);
        purchaseSection.addEventListener('touchcancel', onTouchEnd);

        bookWrapper.addEventListener('click', () => {
            if (!bookRef) return;
            // Ignore clicks that happen during touch (quick taps)
            if (isTouching) return;
            
            front = !front;
            requestAnimationFrame(() => {
                bookRef.setRotation(front ? defaultRotation : 180 + defaultRotation, 0, 0, true);
            })
        });

        // Keyboard accessibility: Allow Enter and Space to flip book
        bookWrapper.addEventListener('keydown', (event: KeyboardEvent) => {
            if (!bookRef) return;
            if (event.key === 'Enter' || event.key === ' ') {
                event.preventDefault();
                front = !front;
                requestAnimationFrame(() => {
                    bookRef.setRotation(front ? defaultRotation : 180 + defaultRotation, 0, 0, true);
                });
            }
        });
    });
</script>

<section class="purchase-section" aria-label="Buch kaufen">
    <div tabindex="0" role="button" aria-label="Buch umdrehen (Enter oder Leertaste drücken)">
        <Book
                bind:this={bookRef}
                coverImage="{book.coverImage}"
                coverImageAlt="Cover: {book.title}"
                backCoverImage="{book.backCoverImage}"
                backCoverImageAlt="Back Cover: {book.title}"
                spineImage="{book.spineImage}"
                depth={20}
                transition={false}
        ></Book>
    </div>

    <aside class="info">
        <h1 class="book-title">{book.title}</h1>
        {#if book.author}
            <div class="book-author">von {book.author}</div>
        {/if}

        <div class="prices">
            <div class="price">
                <div class="label">Hardcover (Farbe)</div>
                <div class="amount">{book.priceHardcover}</div>
            </div>
            <div class="price">
                <div class="label">Taschenbuch (Schwarz/Weiß)</div>
                <div class="amount">{book.priceSoftcover}</div>
            </div>
        </div>

        <div class="actions">
            {#if book.amazonUrl}
                <a class="btn" href="{book.amazonUrl}" target="_blank" rel="noopener noreferrer"
                   aria-label="Auf Amazon kaufen">
                    <AmazonLogo/> Auf Amazon kaufen
                </a>
            {/if}

            {#if book.email}
                <a class="btn" href="mailto:{book.email}?subject=Interesse an {encodeURIComponent(book.title)}"
                   aria-label="Per E‑Mail Bestellen">
                    <MailIcon/> Per E‑Mail bestellen
                </a>
            {/if}
        </div>
    </aside>
</section>

<style>
    .purchase-section {
        position: relative;
        width: 100%;
        min-height: calc(100dvh - var(--footer-height));
        max-width: 1200px;
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        overflow: visible;

        @media screen and (max-width: 720px) {
            flex-direction: column;
            gap: 5rem;

            /*:global(.book) {*/
            /*    transition: transform 0.5s ease;*/
            /*}*/
        }

        [role="button"] {
            cursor: pointer;
            outline: none;
        }

        [role="button"]:focus-visible {
            outline: 3px solid var(--accent, rgba(255, 225, 140, 0.95));
            outline-offset: 8px;
            border-radius: 4px;
        }

        :global(.book) {
            pointer-events: none;
        }

        .info {
            min-width: 240px;
            display: flex;
            flex-direction: column;
            gap: 1rem;
            text-align: center;

            .book-title {
                margin: 0;
            }

            .book-author {
                color: #666;
                margin-top: -1rem;
            }

            .prices {
                display: flex;
                gap: 1rem;
            }

            .price {
                background: transparent;
                border-radius: 8px;
                padding: 0.6rem 0.9rem;
                min-width: 110px;
                text-align: left;
                box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.03);

                .label {
                    font-size: 0.8rem;
                    color: #777;
                }

                .amount {
                    font-weight: 700;
                    margin-top: 0.25rem;
                    font-size: 1.05rem;
                }
            }

            .actions {
                display: flex;
                flex-direction: column;
                gap: 0.75rem;
                /*gap: 12px;*/
                width: 100%;
                margin-top: 0.5rem;
                align-items: center;

                .btn {
                    display: inline-block;
                    padding: 0.6rem 0.9rem;
                    border-radius: 28px; /* 6px */
                    text-decoration: none;
                    font-weight: 600;
                    font-size: 0.95rem;


                    width: 100%;
                    max-width: 440px;

                    color: white;
                    background: rgba(255, 255, 255, 0.09);
                    border: 1px solid rgba(255, 255, 255, 0.18);

                    transition: transform .26s ease, background .2s ease;

                    &:hover {
                        transform: translateY(-4px);
                        background: rgba(255, 255, 255, 0.18);
                    }

                    :global(svg) {
                        width: 1.3em;
                        height: auto;
                        vertical-align: sub;
                        margin-right: 0.2rem;

                        &.feather-at-sign,
                        &.feather-mail {
                            width: 1.1em;
                        }
                    }
                }
            }
        }
    }
</style>
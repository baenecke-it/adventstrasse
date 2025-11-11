<script lang="ts">
    import {onMount} from 'svelte';
    import Book from '../Book.svelte';

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
        const bookEl = purchaseSection?.querySelector<HTMLElement>('.book');
        if (!purchaseSection || !bookEl) return;

        function clamp(num: number, min: number, max: number): number {
            return Math.min(Math.max(num, min), max);
        }

        let front = true;
        window.addEventListener('pointermove', (event: PointerEvent) => {
            if (!bookRef) return;

            const rect = purchaseSection.getBoundingClientRect();
            const centerX = rect.left + rect.width / 2;
            const centerY = rect.top + rect.height / 2;

            const deltaX = event.clientX - centerX;
            const deltaY = event.clientY - centerY;

            const rotateY = clamp((deltaX / (rect.width / 2)) * 30, -40, 40); // Max +-40 degrees
            const rotateX = clamp((-deltaY / (rect.height / 2)) * 10, -15, 15); // Max +-15 degrees

            requestAnimationFrame(() => {
                bookRef.setRotation(rotateY + (front ? 0 : 180), rotateX * (front ? 1 : -1));
            });
        });

        bookEl.addEventListener('click', () => {
            if (!bookRef) return;
            front = !front;
            requestAnimationFrame(() => {
                bookRef.setRotation(front ? 0 : 180, 0);
            })
        });
    });
</script>

<section class="purchase-section" aria-label="Buch kaufen">
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

    <aside class="info">
        <h3 class="book-title">{book.title}</h3>
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
                    📦 Auf Amazon kaufen
                </a>
            {/if}

            {#if book.email}
                <a class="btn" href="mailto:{book.email}?subject=Interesse an {encodeURIComponent(book.title)}"
                   aria-label="Per E‑Mail Bestellen">
                    📬 Per E‑Mail bestellen
                </a>
            {/if}
        </div>
    </aside>
</section>

<style>
    .purchase-section {
        touch-action: pan-y;
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

        :global(.book) {
            cursor: pointer;
        }

        .info {
            min-width: 240px;
            display: flex;
            flex-direction: column;
            gap: 1rem;
            text-align: center;

            .book-title {
                margin: 0;
                font-size: 1.25rem;
            }

            .book-author {
                color: #666;
                font-size: 0.95rem;
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
            }

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
            }
        }
    }
</style>
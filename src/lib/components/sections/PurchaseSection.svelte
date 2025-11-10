<script lang="ts">
    import {onMount} from 'svelte';
    import {scale} from 'svelte/transition';
    import Book from '../Book.svelte';

    interface Book {
        title: string;
        author?: string;
        cover?: string;
        priceHardcover?: string;
        priceSoftcover?: string;
        amazonUrl?: string;
        email?: string;
    }

    export let book: Book = {
        title: 'Beispielbuch',
        author: 'Max Mustermann',
        cover: '', // optional: Pfad zur Cover‑Bilddatei
        priceHardcover: '€24.99',
        priceSoftcover: '€14.99',
        amazonUrl: 'https://www.amazon.de/',
        email: 'sales@example.com'
    };

    let placed = true;
</script>

<div class="shelf">
    <Book
            spineImageAlt=""
            initialRotation={90}
            shadow={false}
            hover={false}
            containerWidth={43}
            scale={1.55}
            coverColor="teal"
    ></Book>
    <Book
            spineImageAlt=""
            initialRotation={90}
            shadow={false}
            hover={false}
            containerWidth={43}
            scale={1.5}
            coverColor="navy"
    ></Book>
    <Book
            spineImageAlt=""
            initialRotation={90}
            shadow={false}
            hover={false}
            containerWidth={40}
            scale={1.2}
    ></Book>
    <Book
            spineImageAlt=""
            initialRotation={90}
            shadow={false}
            hover={false}
            containerWidth={40}
            scale={1.3}
            coverColor="green"
    ></Book>
    <Book
            spineImageAlt=""
            initialRotation={90}
            shadow={false}
            hover={false}
            containerWidth={40}
            scale={1.1}
            coverColor="blue"
    ></Book>
    <div class="shelf-board"></div>
</div>

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
            <a class="btn amazon" href="{book.amazonUrl}" target="_blank" rel="noopener noreferrer"
               aria-label="Auf Amazon kaufen">
                Auf Amazon kaufen
            </a>
        {/if}

        {#if book.email}
            <a class="btn mail" href="mailto:{book.email}?subject=Interesse an {encodeURIComponent(book.title)}"
               aria-label="Per E‑Mail Bestellen">
                Per E‑Mail bestellen
            </a>
        {/if}
    </div>
</aside>

<style>
    .shelf {
        position: absolute;
        bottom: 13%;
        width: 50%;
        left: 50%;
        transform: translateX(-56%);
        height: 260px;
        display: flex;
        align-items: flex-end;
        justify-content: center;

        :global(.book) {
            bottom: 16.6%;
        }

        .shelf-board {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            height: 30px;
            background-image: url("$lib/assets/wood-pattern.png");
            background-color: #7d3a00;
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.25);
            border-top: 2px solid rgba(255, 255, 255, 0.06);
        }
    }

    .info {
        position: absolute;
        top: 50%;
        left: 60%;
        transform: translate(0, -50%);
        min-width: 240px;
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }

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
        background: #f7f7f7;
        border-radius: 8px;
        padding: 0.6rem 0.9rem;
        min-width: 110px;
        text-align: left;
        box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.03);
    }

    .price .label {
        font-size: 0.8rem;
        color: #777;
    }

    .price .amount {
        font-weight: 700;
        margin-top: 0.25rem;
        font-size: 1.05rem;
    }

    .actions {
        display: flex;
        gap: 0.75rem;
        margin-top: 0.5rem;
    }

    .btn {
        display: inline-block;
        padding: 0.6rem 0.9rem;
        border-radius: 6px;
        text-decoration: none;
        color: white;
        font-weight: 600;
        font-size: 0.95rem;
    }

    .btn.amazon {
        background: linear-gradient(180deg, #ff8c00, #c85e00);
    }

    .btn.mail {
        background: linear-gradient(180deg, #4a90e2, #2f6fb2);
    }

    @media (max-width: 720px) {
        .shelf-wrapper {
            flex-direction: column;
            align-items: center;
        }

        .shelf {
            width: 280px;
            height: 220px;
        }

        .info {
            width: 100%;
            padding: 0 1rem;
        }
    }
</style>
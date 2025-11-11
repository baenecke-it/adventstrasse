<footer class="footer">
    <p class="copyright">
        © {new Date().getFullYear()} Dorothea Schaller
    </p>
    <nav class="footer-nav">
        <a href="/impressum">Impressum</a>
    </nav>
</footer>

<style>
    .footer {
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        padding: 0.5rem 1rem;
        height: var(--footer-height, 40px);
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap;
        gap: 0.25rem;
        background: rgba(0, 0, 0, 0.3);
        backdrop-filter: blur(10px);
        border-top: 1px solid rgba(255, 255, 255, 0.1);
        z-index: 101;
        box-sizing: border-box;
    }

    .copyright {
        margin: 0;
        color: rgba(255, 255, 255, 0.7);
    }

    .footer-nav {
        display: flex;
        gap: 1rem;
    }

    .footer-nav a {
        color: rgba(255, 255, 255, 0.9);
        text-decoration: none;
        transition: color 0.2s ease;
    }

    .footer-nav a:hover {
        color: var(--accent, rgba(255, 225, 140, 0.95));
    }
</style>

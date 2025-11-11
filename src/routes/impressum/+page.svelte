<svelte:head>
    <title>Impressum – Adventstraße</title>
</svelte:head>

<section class="impressum-page">
    <div class="content-card">
    	<h1>Impressum</h1>

    	<section>
    		<h2>Angaben gemäß § 5 TMG</h2>
    		<p>
    			Dorothea Schaller<br />
    			[Adresse]<br />
    			[PLZ, Ort]
    		</p>
    	</section>

    	<section>
    		<h2>Kontakt</h2>
    		<p>
    			E-Mail: <a href="mailto:adventstrasse@mail.de">adventstrasse@mail.de</a>
    		</p>
    	</section>

    	<section>
    		<h2>Haftungsausschluss</h2>

    		<h3>Haftung für Inhalte</h3>
    		<p>
    			Die Inhalte unserer Seiten wurden mit größter Sorgfalt erstellt. Für die Richtigkeit,
    			Vollständigkeit und Aktualität der Inhalte können wir jedoch keine Gewähr übernehmen. Als
    			Diensteanbieter sind wir gemäß § 7 Abs.1 TMG für eigene Inhalte auf diesen Seiten nach den
    			allgemeinen Gesetzen verantwortlich.
    		</p>

    		<h3>Haftung für Links</h3>
    		<p>
    			Unser Angebot enthält Links zu externen Webseiten Dritter, auf deren Inhalte wir keinen
    			Einfluss haben. Deshalb können wir für diese fremden Inhalte auch keine Gewähr übernehmen.
    			Für die Inhalte der verlinkten Seiten ist stets der jeweilige Anbieter oder Betreiber der
    			Seiten verantwortlich.
    		</p>

    		<h3>Urheberrecht</h3>
    		<p>
    			Die durch die Seitenbetreiber erstellten Inhalte und Werke auf diesen Seiten unterliegen dem
    			deutschen Urheberrecht. Die Vervielfältigung, Bearbeitung, Verbreitung und jede Art der
    			Verwertung außerhalb der Grenzen des Urheberrechtes bedürfen der schriftlichen Zustimmung
    			des jeweiligen Autors bzw. Erstellers.
    		</p>
    	</section>

    	<a href="/" class="back-link">← Zurück zur Startseite</a>
    </div>
</section>

<style>
    .impressum-page {
    	min-height: calc(100vh - var(--footer-height));
    	display: flex;
    	align-items: center;
    	justify-content: center;
    	padding: 4rem 2rem;
    	position: relative;
    	z-index: 10;
    }

    .content-card {
    	background: var(--card-bg);
    	border: 1px solid rgba(255, 255, 255, 0.1);
    	border-radius: 12px;
    	padding: 3rem;
    	max-width: 800px;
    	width: 100%;
    	box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
    	margin: auto;
    }

    h1 {
    	font-family: 'Cormorant Garamond', serif;
    	font-size: 2.5rem;
    	font-weight: 600;
    	margin: 0 0 2rem 0;
    	color: var(--accent);
    }

    h2 {
    	font-family: 'Cormorant Garamond', serif;
    	font-size: 1.5rem;
    	font-weight: 600;
    	margin: 2rem 0 1rem 0;
    	color: rgba(255, 255, 255, 0.95);
    }

    h3 {
    	font-size: 1.1rem;
    	font-weight: 600;
    	margin: 1.5rem 0 0.5rem 0;
    	color: rgba(255, 255, 255, 0.9);
    }

    p {
    	line-height: 1.7;
    	margin: 0.5rem 0;
    	color: rgba(255, 255, 255, 0.85);
    }

    a {
    	color: var(--accent);
    	text-decoration: none;
    	transition: opacity 0.2s ease;
    }

    a:hover {
    	opacity: 0.8;
    }

    .back-link {
    	display: inline-block;
    	margin-top: 2rem;
    	padding: 0.75rem 1.5rem;
    	background: rgba(255, 255, 255, 0.09);
    	border: 1px solid rgba(255, 255, 255, 0.18);
    	border-radius: 28px;
    	color: white;
    	text-decoration: none;
    	font-weight: 600;
    	transition:
    		transform 0.26s ease,
    		background 0.2s ease;
    }

    .back-link:hover {
    	transform: translateY(-2px);
    	background: rgba(255, 255, 255, 0.18);
    }

    @media screen and (max-width: 720px) {
    	.impressum-page {
    		padding: 2rem 1rem;
    	}

    	.content-card {
    		padding: 2rem 1.5rem;
    	}

    	h1 {
    		font-size: 2rem;
    	}

    	h2 {
    		font-size: 1.3rem;
    	}
    }
</style>

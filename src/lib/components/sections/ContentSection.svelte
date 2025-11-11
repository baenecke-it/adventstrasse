<script>
</script>

<section class="content-section" aria-label="Buchbeschreibung">
    <div class="card">
        <h1>Adventstraße – Der Düsterweg erwacht</h1>

        <div class="lead">
            <p>
                Unscheinbar am Rande der Stadt, liegt der Düsterweg – eine graue Straße mit schiefen Zäunen,
                trostlosen Vorgärten und griesgrämigen Nachbarn, die einander längst nichts mehr zu sagen haben.
                Die Herzen sind schwer, die dicken Vorhänge zugezogen und abweisend.
                Es ist der erste Dezember, als ein geheimnisvoller roter Brief seinen Weg auf die Fußmatte
                des Klavierspielers findet – ohne Absender, jedoch mit einer merkwürdigen Aufgabe.
                Am nächsten Tag folgt ein weiterer Brief und dann noch einer ...
                und plötzlich gerät in einer Straße voller verschlossener Türen etwas in Bewegung.
                Mit jedem Brief wächst in den Bewohnern die Ahnung, dass in diesem Advent etwas ganz Besonderes
                vor sich geht.
            </p>
            <p>
                Ein Adventskalender, der das Herz erwärmt und die Leser verzaubert.
            </p>
        </div>
    </div>
</section>

<style>
    .content-section {
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: calc(100dvh - var(--footer-height));

        .card {
            position: relative;
            z-index: 4;
            width: min(820px, 92%);
            padding: 1.25rem;
            display: flex;
            flex-direction: column;
            gap: 1rem;
            align-items: center;
        }

        h1 {
            font-family: 'Cormorant Garamond', serif;
            font-size: 2.4rem;
            margin: 0;
            letter-spacing: 0.8px;
            text-align: center;
        }

        div.lead {
            max-width: 760px;
            margin: 0;
            font-family: 'Cormorant Garamond', serif;
            font-size: 1rem;
            line-height: 1.5;
            background: var(--card-bg);
            padding: 1rem 1.5rem;
            border-radius: 12px;
            text-align: center;
        }

        @media (max-width: 720px) {
            h1 {
                font-size: 1.8rem
            }
        }
    }
</style>
<script>
    import authorImage from "$lib/assets/author_dorothea_schaller.png";

    export let name = "Dorothea Schaller";
    export let role = "Autorin";
    export let bio = "Dorothea Schaller wurde 1994 in Illertissen geboren. Nach ihrem Abitur und einer Ausbildung im Bereich\n" +
        " Tourismusmanagement arbeitete sie für einige Jahre in der Gastronomie und Eventbranche in der Schweiz. Dort\n" +
        " entdeckte sie ihre Liebe zum Schreiben. Neben dem Lesen spannender Bücher und dem Organisieren spektakulärer\n" +
        " Events liebt Dorothea Schaller es zu reisen. Während einer Rundreise durch Neuseeland und Indonesien,\n" +
        " entstanden ihre ersten Kinderbuchillustrationen. Die Idee für ihr Buch „die Adventstraße“ kam Dorothea\n" +
        " Schaller\n" +
        " bei einer Zugfahrt entlang des Zürichsees.\n" +
        " Schon seit Kindertagen ist für sie die Vorweihnachtszeit eine der schöns-ten Zeiten im Jahr. Der erste\n" +
        " Schnee,\n" +
        " die vielen Lichter und die alten Rituale, wie das Plätzchen backen und Wohnung schmücken, machen für sie\n" +
        " den\n" +
        " Advent zu etwas ganz Besonderem. Mit ihrem Buch schaffte sie es, eine neue Tradition in ihrer Familie zu\n" +
        " etablieren. An jedem Abend im Advent werden nun die Lichter gedimmt, Plätzchen bereitgestellt und der\n" +
        " Adventskranz entzündet. Dann setzen sich alle zusammen und lauschen einer neuen Adventsgeschichte";
</script>

<section class="author-section" aria-label="Über die Autorin">
    <h2 class="section-title">Über mich</h2>
    <article class="author-card" role="article">
        <figure class="author-figure">
            <img src={authorImage} alt={name} class="author-image"/>
            <figcaption class="author-meta">
                <h3 class="author-name">{name}</h3>
                <span class="author-role">{role}</span>
            </figcaption>
        </figure>

        <div class="author-bio">
            <p class="description">{bio}</p>
        </div>
    </article>
</section>

<style>
    .author-section {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        min-height: calc(100dvh - var(--footer-height));

        .author-card {
            width: min(820px, 92%);
            display: grid;
            grid-template-columns: 160px 1fr;
            gap: 1.25rem;
            align-items: center;
            background: var(--card-bg);
            padding: 1.25rem;
            border-radius: 12px;
            box-shadow: 0 6px 18px rgba(16, 24, 40, 0.06);
            border: 1px solid rgba(0, 0, 0, 0.03);

            .author-figure {
                display: flex;
                flex-direction: column;
                align-items: center;
                margin: 0;
                gap: 0.5rem;
                text-align: center;

                .author-image {
                    width: 140px;
                    height: 140px;
                    border-radius: 50%;
                    object-fit: cover;
                    border: 3px solid #fff;
                    box-shadow: 0 8px 20px rgba(16, 24, 40, 0.08);
                    background: linear-gradient(180deg, #fff, #f7fafc);
                }

                .author-meta {
                    display: block;

                    .author-name {
                        margin: 0;
                    }

                    .author-role {
                        display: block;
                        font-size: 0.875rem;
                        color: var(--muted);
                    }
                }
            }

            .author-bio {
                padding: 0.25rem 0;

                .description {
                    margin: 0;
                    line-height: 1.5;
                    text-align: left;
                }
            }

            @media (max-width: 720px) {
                & {
                    grid-template-columns: 1fr;
                    text-align: center;
                    padding: 1rem;

                    .author-bio {
                        padding-top: 0.5rem;

                        .description {
                            text-align: center;
                        }
                    }
                }
            }
        }
    }
</style>
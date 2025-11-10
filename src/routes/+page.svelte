<script lang="ts">
    import Book from "$lib/components/Book.svelte";
    import coverImage from "$lib/assets/cover_adventstrasse.jpg";
    import backCoverImage from "$lib/assets/backcover_adventstrasse.jpg";
    import spineImage from "$lib/assets/spine_adventstrasse.jpg";
    import {onMount} from "svelte";
    import {gsap} from "gsap";
    import {MotionPathPlugin} from "gsap/MotionPathPlugin";
    import {Observer} from "gsap/Observer";
    import {ScrollTrigger} from "gsap/ScrollTrigger";
    import Section from "$lib/components/sections/Section.svelte";
    import ContentSection from "$lib/components/sections/ContentSection.svelte";
    import AuthorSection from "$lib/components/sections/AuthorSection.svelte";

    let isMobile: boolean = false;

    onMount(() => {
        gsap.registerPlugin(MotionPathPlugin, Observer, ScrollTrigger);

        const bookContainer = document.querySelector('#book-container') as HTMLElement | null;
        const bookEl = bookContainer?.querySelector<HTMLElement>('.book') ?? null;
        const sections = Array.from(document.querySelectorAll<HTMLElement>('.scroll-section'));
        if (!bookContainer || !bookEl || sections.length === 0) return;

        let tl: gsap.core.Timeline | null = null;

        let currentIndex = 0;

        const clampedIndex = (index: number) => {
            return Math.min(Math.max(0, index), sections.length - 1);
        };

        let animating = false;
        const gotoSection = (sectionIndex: number, mobile: boolean = false, force: boolean = false) => {
            const direction = clampedIndex(sectionIndex) % 2 === 0;
            const currentSection = sections[clampedIndex(currentIndex)];
            const nextSection = sections[clampedIndex(sectionIndex)];

            if (!force && (currentIndex === clampedIndex(sectionIndex))) {
                return; // No change
            }

            animating = true;

            if (tl) {
                tl.kill();
                tl = null;
            }

            tl = gsap.timeline({
                defaults: {
                    duration: .5,
                    ease: 'none',
                },
                onComplete: () => {
                    animating = false;
                }
            });

            if (!force) {
                tl.to(bookEl, {
                    rotationY: 90,
                }, 0);
            }
            tl.to(bookEl, {
                rotationY: direction ? -30 : 210,
            }, force ? 0 : .5);

            if (!mobile) {
                tl
                    .to(bookContainer, {
                        left: '50%',
                    }, 0)
                    .to(nextSection, {
                        width: mobile ? '100vw' : '50vw',
                    }, .3)
                    .to(currentSection, {
                        width: 0,
                    }, .2)
                    .to(bookContainer, {
                        left: direction ? '75%' : '25%',
                    }, .5);
            }

            currentIndex = clampedIndex(sectionIndex);
        };

        // create
        let mm = gsap.matchMedia();

        // add a media query. When it matches, the associated function will run
        mm.add("(min-width: 769px)", () => {
            gsap.set(bookContainer, {left: '50%'});
            return gotoSection(0);
        });

        mm.add("(min-width: 769px)", () => {
            Observer.create({
                type: "wheel,touch,pointer",
                onUp: () => {
                    if (animating) return;

                    gotoSection(currentIndex - 1);

                },
                onDown: () => {
                    if (animating) return;
                    gotoSection(currentIndex + 1);
                },
                tolerance: 5
            });
        });

        mm.add("(max-width: 768px)", () => {
            ScrollTrigger.create({
                trigger: bookContainer,
                start: "center center",
                scrub: true,
                onToggle: self => {
                    const sectionIndex = clampedIndex(currentIndex + (self.isActive ? 1 : -1));
                    if (animating) return;
                    gotoSection(sectionIndex, true);
                },
            });
        });

        bookContainer.style.visibility = 'visible';

        function onResize() {
            const wasMobile = isMobile;
            if (window.innerWidth >= 769) {
                isMobile = false;
            } else {
                isMobile = true;
            }
            console.log(`wasMobile`, wasMobile);
            console.log(`isMobile`, isMobile);
            console.log(`wasMobile !== isMobile`, wasMobile !== isMobile);
            gotoSection(currentIndex, isMobile, wasMobile !== isMobile);
        }

        onResize();
        window.onresize = onResize;

        return () => {
            if (tl) tl.kill();
        };
    });
</script>

<Section id="book-description" offsetX="75%" rotation={-30}>
    <ContentSection></ContentSection>
</Section>
<div id="book-container">
    <Book
            {coverImage}
            coverImageAlt="Cover: Die Adventstraße (Dorothea Schaller)"
            backCoverImage="{backCoverImage}"
            backCoverImageAlt="Back Cover: Die Adventstraße (Dorothea Schaller)"
            spineImage="{spineImage}"
            scale={isMobile ? 1 : 2}
            shadow={false}
            transition={false}
    ></Book>
</div>
<Section id="author-description" anchor=".6" offsetX="25%" rotation={200} right={true}>
    <AuthorSection></AuthorSection>
</Section>

<style>

    #book-container {
        visibility: hidden; /* Hide until onMount */
        position: absolute;
        top: 50%;
        left: 75%;
        transform: translate(-50%, -50%);
        display: flex;
        justify-content: center;

        @media (max-width: 768px) {
            position: relative;
            transform: translate(-50%, 0);
            margin-top: 2rem;
            left: 50%;
        }
    }
</style>
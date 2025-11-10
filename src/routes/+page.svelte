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
    import {CustomEase} from "gsap/CustomEase";
    import Section from "$lib/components/sections/Section.svelte";
    import ContentSection from "$lib/components/sections/ContentSection.svelte";
    import AuthorSection from "$lib/components/sections/AuthorSection.svelte";
    import PurchaseSection from "$lib/components/sections/PurchaseSection.svelte";

    let isMobile: boolean = false;

    onMount(() => {
        gsap.registerPlugin(MotionPathPlugin, Observer, ScrollTrigger, CustomEase);

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
            tl
                .to(bookEl, {
                    rotationY: direction ? -30 : 210,
                }, force ? 0 : .5)
                .to(bookContainer, {
                    left: '50%',
                }, 0)
                .to(bookContainer, {
                    left: direction ? '75%' : '25%',
                }, .5);

            currentIndex = clampedIndex(sectionIndex);
        };

        const sectionDuration = 1; // seconds per section

        // create
        let mm = gsap.matchMedia();

        // add a media query. When it matches, the associated function will run
        mm.add({
            isMobile: "(max-width: 768px)",
            isDesktop: "(min-width: 769px)"
        }, () => {
            if (isMobile) {
                gsap.set(bookContainer, {left: '50%'});
            } else {
                let tl = gsap.timeline({
                    scrollTrigger: {
                        trigger: "body",
                        start: "top top",
                        end: "bottom bottom+=67%",
                        scrub: true
                    },
                    defaults: {duration: sectionDuration, ease: 'none'}
                });

                let delay = 0;
                sections.forEach((section, index) => {
                    if (index === 0) {
                        tl.set(bookEl, {
                            rotationY: section.dataset.rotation,
                            scale: section.dataset.scale,
                        }, delay);
                        tl.set(bookContainer, {
                            left: section.dataset.offsetX,
                        }, delay);
                    } else {
                        if (section.id === 'buy') {
                        }

                        tl.to(bookEl, {
                            rotationY: section.dataset.rotation,
                            scale: section.dataset.scale,
                            // ease: CustomEase.create("custom", "M0,0 C0,0 1,0.5 1,0.5 ")
                        }, delay + '+=70%');
                        tl.to(bookContainer, {
                            left: section.dataset.offsetX,
                        }, delay + '+=70%');
                        delay += sectionDuration;
                    }
                });
            }
        });

        bookContainer.style.visibility = 'visible';

        function onResize() {
            const wasMobile = isMobile;
            if (window.innerWidth >= 769) {
                isMobile = false;
            } else {
                isMobile = true;
            }
            gotoSection(currentIndex, isMobile, wasMobile !== isMobile);
        }

        // onResize();
        // window.onresize = onResize;

        return () => {
            if (tl) tl.kill();
        };
    });
</script>

<Section id="book-description" offsetX="75%" rotation={-30} scale={1}>
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
            depth={20}
    ></Book>
</div>
<Section id="author-description" anchor=".6" offsetX="25%" rotation={200} right={true} scale={1}>
    <AuthorSection></AuthorSection>
</Section>
<Section id="buy" anchor=".6" offsetX="35%" rotation={90} scale={.75} right={null}>
    <PurchaseSection
            book={{
                title: 'Die Adventstraße',
                author: 'Dorothea Schaller',
                cover: coverImage,
                priceHardcover: '15,99 €',
                priceSoftcover: '9,99 €',
                amazonUrl: 'https://amzn.eu/d/ePQiZNm',
                email: 'adventstrasse@mail.de'
            }}
    ></PurchaseSection>
</Section>

<style>

    #book-container {
        visibility: hidden; /* Hide until onMount */
        position: fixed;
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
<script lang="ts">
    import coverImage from "$lib/assets/cover_adventstrasse.jpg";
    import backCoverImage from "$lib/assets/backcover_adventstrasse.jpg";
    import spineImage from "$lib/assets/spine_adventstrasse.jpg";
    import PurchaseSection from "$lib/components/sections/PurchaseSection.svelte";
    import ContentSection from "$lib/components/sections/ContentSection.svelte";
    import AuthorSection from "$lib/components/sections/AuthorSection.svelte";
</script>

<svelte:head>
    <title>Adventstraße – Der Düsterweg erwacht</title>
</svelte:head>


<PurchaseSection
        book={{
                title: 'Die Adventstraße',
                author: 'Dorothea Schaller',
                coverImage: coverImage,
                spineImage: spineImage,
                backCoverImage: backCoverImage,
                priceHardcover: '15,99 €',
                priceSoftcover: '9,99 €',
                amazonUrl: 'https://amzn.eu/d/ePQiZNm',
                email: 'adventstrasse@mail.de'
            }}
></PurchaseSection>
<ContentSection></ContentSection>
<AuthorSection></AuthorSection>


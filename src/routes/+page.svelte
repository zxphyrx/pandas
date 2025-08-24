<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";

    import ZooBanner from "$lib/assets/Zoo.svelte";
    import Hero from "$lib/assets/Hero.svelte";
    import About from "$lib/assets/About.svelte";
    import Vulnerable from "$lib/assets/Vulnerable.svelte";
    import Facts from "$lib/assets/Facts.svelte";
    import Panda from "$lib/assets/Panda.svelte";

    gsap.registerPlugin(ScrollTrigger);
    
    onMount(() => {
        let aboutSection = document.querySelector(".about");
        let vulnSection = document.querySelector(".vulnerable");
        let factsSection = document.querySelector(".facts");

        ScrollTrigger.create({
            trigger: aboutSection,
            start: "top top",
            endTrigger: vulnSection,
            end: "top top",
            pin: true,
            pinSpacing: false
        })

        ScrollTrigger.create({
            trigger: vulnSection,
            start: "top top",
            endTrigger: factsSection,
            end: "top top",
            pin: true,
            pinSpacing: false
        })
    })
</script>

<style>
</style>

<svelte:head>
    <title>pandas</title>
</svelte:head>

<ZooBanner></ZooBanner>
<Hero></Hero>
<About></About>
<Vulnerable></Vulnerable>
<Facts></Facts>
<Panda></Panda>
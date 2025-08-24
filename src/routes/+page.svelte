<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/all";

    import ZooBanner from "$lib/assets/Zoo.svelte";
    import Hero from "$lib/assets/Hero.svelte";
    import About from "$lib/assets/About.svelte";
    import Vulnerable from "$lib/assets/Vulnerable.svelte";
    import Facts from "$lib/assets/Facts.svelte";
    import Panda from "$lib/assets/Panda.svelte";

    let sections = [];
    
    onMount(() => {
    gsap.registerPlugin(ScrollTrigger);
    
        sections = document.querySelectorAll(".section");

        sections.forEach((section, index) => {
            if(index >= sections.length) return;
            let nextSection = sections[index + 1];
            gsap.to(section, {
                trigger: section,
                start: "top top",
                endTrigger: nextSection,
                end: "top top",
                pin: section
            })
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
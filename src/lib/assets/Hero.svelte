<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/all";

    let heroSection;
    let heroMountains;
    let heroTitle;
    let heroFog;
    let heroPin;

    gsap.registerPlugin(ScrollTrigger);
    
    onMount(() => {
        gsap.timeline({
            scrollTrigger: {
                trigger: heroSection,
                start: "top top",
                endTrigger: heroSection,
                end: "bottom bottom",
                scrub: true,
                pin: heroTitle
            }
        })
        .fromTo(heroFog, {
            
        })
    })
    
</script>


<style lang="scss">
    .hero {
        height: fit-content;

        div#mountains {
            height: fit-content;
            width: fit-content;
            position: relative;
            z-index: 1;

            img#mountainsImg {
                height: auto;
                width: 100%;
                margin-top: 10vh;
            }

            div#mountainsFade {
                position: absolute;
                inset: 0;
                background-image: linear-gradient(to bottom, transparent 70%, black 100%);
                pointer-events: none;
                height: 100%;
            }
        }
        
        img#fogImg {
            height: auto;
            width: 100vw;
            position: fixed;
            top: 0;
            left: 0;
            z-index: 2;
            mix-blend-mode: screen;
            background-image: linear-gradient(to bottom, transparent 70%, black 100%);
        }
        
        h1 {
            text-align: center;
            font-size: 4rem;
            transform: translateY(calc(50vh - 8rem));
            margin: 0;
            z-index: 0;
        }
    }
</style>

<div bind:this={heroSection} class="hero section">

    <img bind:this={heroFog} id="fogImg" src="/fog/1.jpg">
    <h1 bind:this={heroTitle}>the giant panda</h1>
    <div id="mountains">
        <img id="mountainsImg" bind:this={heroMountains} src="/mountains.png" alt="mountains">
        <div id="mountainsFade"></div>
    </div>
</div>
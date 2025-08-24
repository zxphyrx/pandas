<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";

    let heroSection;
    let heroMountains;
    let heroTitle;
    let heroFog1;
    let heroFog2;
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
        .fromTo(heroFog1,
            {
                top: "40vh"
            },
            {
                top: 0,
                duration: 1
            },
        0)
        .fromTo(heroFog2,
            {
                top: "40vh"
            },
            {
                top: 0,
                duration: 2
            },
        0)
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
                background-image: linear-gradient(to bottom, transparent 70%, rgb(8, 8, 8) 100%);
                pointer-events: none;
                height: 100%;
            }
        }
        
        img.fogImg {
            height: auto;
            width: 100vw;
            position: absolute;
            top: 0;
            z-index: 2;
            mix-blend-mode: screen;
        }

        img.fogImg#fog1 {
            left: -40vw;
        }
        
        img.fogImg#fog2 {
            width: 50vw;
            left: 60vw;
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
    <img bind:this={heroFog1} class="fogImg" id="fog1" src="/fog/1.png">
    <img bind:this={heroFog2} class="fogImg" id="fog2" src="/fog/2.png">
    <h1 bind:this={heroTitle}>the giant panda</h1>
    <div id="mountains">
        <img id="mountainsImg" bind:this={heroMountains} src="/mountains.png" alt="mountains">
        <div id="mountainsFade"></div>
    </div>
</div>
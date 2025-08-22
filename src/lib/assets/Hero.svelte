<style lang="scss">
    .hero {
        height: fit-content;

        div#mountains {
            height: fit-content;
            width: fit-content;
            position: relative;

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
                aspect-ratio: 3 / 2;
            }
        }
        
        h1 {
            text-align: center;
            font-size: 4rem;
            transform: translateY(calc(50vh - 8rem));
            margin: 0;
        }
    }
</style>

<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/all";

    let heroSection;
    let heroMountains;
    let heroTitle;

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
        .fromTo(heroMountains,
            {
                marginTop: "10vh"
            },
            {
                marginTop: "0vh",
                duration: 1
            }
        )
    })
</script>

<div bind:this={heroSection} class="hero section">
    <h1 bind:this={heroTitle}>the giant panda</h1>
    <div id="mountains">
        <img id="mountainsImg" bind:this={heroMountains} src="/mountains.png" alt="mountains">
        <div id="mountainsFade"></div>
    </div>
</div>
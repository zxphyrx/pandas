<style lang="scss">
    .hero {
        background-color: skyblue;
        height: 500vh;

        img {
            height: auto;
            width: 100%;
            z-index: 1;
            transform: translateY(50vh);
        }
        
        h1 {
            text-align: center;
            font-size: 8rem;
            transform: translateY(40vh);
        }
    }
</style>

<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/all";

    let heroSection;
    let heroImage;
    let heroTitle;

    gsap.registerPlugin(ScrollTrigger);
    
    onMount(() => {
        gsap.timeline({
            scrollTrigger: {
                trigger: heroSection,
                start: "top top",
                end: "bottom top",
                scrub: true,
                markers: true
            }
        })
        .fromTo(heroImage,
            {
                y: "40vh"
            },
            {
                y: "0vh",
                duration: 1
            }
        )
        .fromTo(heroTitle,
            {
                y: "40vh"
            },
            {
                y: "0vh",
                duration: 0.2
            }
        )
    })
</script>

<div bind:this={heroSection} class="hero section">
    <h1 bind:this={heroTitle}>panda!!</h1>
    <img bind:this={heroImage} src="/mountain.png" alt="mountain">
</div>
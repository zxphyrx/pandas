<style lang="scss">
    .section {
        align-items: start;
        justify-content: left;
        padding-top: 50vh;
        z-index: 2;
    }

    .panel {
        width: fit-content;
        display: flex;
        flex-direction: row;
    }

    .fact {
        display: flex;
        flex-direction: column;
        width: 100vw;
        justify-content: center;
        align-items: center;
    }
</style>
<script>
    import { onMount, tick } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";

    let facts = [];
    let panelElem;
    let factsEnd;
    let factsWidth;
    let factsScrollSpeed = 0.5;

    gsap.registerPlugin(ScrollTrigger);
    
    onMount(async () => {
        fetch("/facts.json")
        .then((res) => {
            return res.json();
        })
        .then((json) => {
            facts = json;
        })

        await tick();
    })

    $: if(facts.length && panelElem) {
        factsWidth = (facts.length - 1) * window.innerWidth;

        gsap.fromTo(panelElem,
            {
                x: 0
            },
            {
                scrollTrigger: {
                    trigger: panelElem,
                    start: "center center",
                    endTrigger: factsEnd,
                    end: "bottom bottom",
                    scrub: true,
                    pin: true
                },
                x: -factsWidth
            }
        )
    }

</script>

<div class="facts section">
    <div bind:this={panelElem} class="panel">
        {#each facts as fact}
            <div class="fact">
                <h2>
                    {fact.title}
                </h2>
                <p>
                    {fact.text}
                </p>
            </div>
        {/each}
    </div>
    <div bind:this={factsEnd} style="height: {(factsWidth / 2) / factsScrollSpeed}px"></div>
</div>
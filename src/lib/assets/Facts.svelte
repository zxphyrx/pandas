<style lang="scss">
    .section {
        align-items: start;
        justify-content: left;
        z-index: 2;
    }

    .panel {
        width: fit-content;
        display: flex;
        flex-direction: row;
    }

    .fact {
        height: 100vh;
        width: 100vw;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-size: 100%;
        background-repeat: no-repeat;

        .fact-text {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background-color: rgba(8, 8, 8, 0.75);
            backdrop-filter: blur(10px);
            padding: 32px;
            border-radius: 16px;

            h2 {
                font-size: 2rem;
            }

            p {
                font-size: 1.25rem;
            }
        }
    }
</style>

<script>
    import { onMount, tick } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";
    import { base } from "$app/paths";

    const shuffle = a=>a.sort(()=>Math.random()-0.5);

    let facts = [];
    let panelElem;
    let factsEnd;
    let factsWidth;
    let factsScrollSpeed = 0.5;
    let imgPath = "pandas";
    let pandaImgs = shuffle([1, 2, 3, 4]);

    if(Math.floor(Math.random() * 100) == 1) {
        imgPath = "cats";
    }

    gsap.registerPlugin(ScrollTrigger);
    
    onMount(async () => {
        fetch(`${base}/facts.json`)
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
        {#each facts as fact, factIndex}
            <!-- svelte-ignore a11y_no_static_element_interactions -->
            <div class="fact" style="background-image: url('{base}/{imgPath}/{pandaImgs[factIndex]}.jpg');">
                <div class="fact-text">
                    <h2>
                        {fact.title}
                    </h2>
                    <p>
                        {fact.text}
                    </p>
                </div>
            </div>
        {/each}
    </div>
    <div bind:this={factsEnd} style="height: {(factsWidth / 2) / factsScrollSpeed}px"></div>
</div>
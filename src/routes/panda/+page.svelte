<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/all";

    import Panda from "$lib/assets/panda/Panda.svelte";

    onMount(() => {
        gsap.registerPlugin(ScrollTrigger);
    })
</script>

<style>
</style>

<svelte:head>
    <title>pandas</title>
</svelte:head>

<Panda></Panda>
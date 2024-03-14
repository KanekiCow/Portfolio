<script lang="ts">
    import { onMount } from "svelte";
    import Typed from "typed.js";

    let element: HTMLElement;

    onMount(() => {
        const typed = new Typed(element, {
            strings: ["Your", "Mom"],
            typeSpeed: 70,
        });

        // when unmounted
        return () => {
            typed.destroy();
        }
    });
</script>

<span bind:this={element} />
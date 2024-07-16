<script lang="ts">
  import { onMount } from "svelte";
  import tilt from "vanilla-tilt";
  import Artist from "./Artist.svelte";
  import Cover from "./Cover.svelte";
  import Tittle from "./Tittle.svelte";

  export let title: string = "";
  export let artist: string = "";
  export let cover: string = "";

 onMount(() => {
    const elements = document.querySelectorAll('.tilt');
    if (elements) {
      tilt.init(Array.from(elements) as HTMLElement[], {
        scale:1.1,
        max: 25,
        speed: 400,
        glare: true,
        'max-glare': 0.1
      });
    }
  });
</script>

<div
  
  class=" tilt bg-black/30 hover:bg-black/50 border-[2px] border-gray-600/40 hover:border-[#764ADE] w-fit max-w-[170px] p-5 rounded-lg transition-all duration-[250ms] ease-in-out "
>

  <Cover text={cover} />
  <Tittle text={title} />
  <Artist text={artist} />
</div>

 <style>
  .tilt {
    transform-style: preserve-3d;
    transform: perspective(1000px);
  }
 </style>
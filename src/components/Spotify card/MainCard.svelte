<script lang="ts">
  import Artist from "./Artist.svelte";
  import Cover from "./Cover.svelte";
  import Tittle from "./Tittle.svelte";

  export let title: string = "";
  export let artist: string = "";
  export let cover: string = "";
</script>

<div
  class="bg-black/30 overflow-hidden hover:bg-black/50 border-[2px] border-gray-600/40 hover:border-[#764ADE] w-fit max-w-[170px] p-5 rounded-lg hover:z-50 hover:translate-y-[-100px] hover:scale-[1.3] transition-all duration-[150ms] ease-in-out hover:rotate-6 hover:backdrop-blur-3xl hover:shadow-2xl "
>
  <Cover text={cover} />
  <Tittle text={title} />
  <Artist text={artist} />
</div>

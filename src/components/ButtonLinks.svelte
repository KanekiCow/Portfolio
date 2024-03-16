<script lang="ts">
  export let links: { label: string; url: string; }[] = [];

  function handleClick(url: string) {
    window.open(url, "_blank");
  }
</script>

<div class="flex flex-row space-x-3 mt-5">
  {#each links as link}
    <button on:click={() => handleClick(link.url)} class="h-[34px] item p-[5px] px-[10px] rounded-lg active:scale-[.85] ease-linear transition-all duration-100 flex flex-row justify-center items-center bg-black/20">{link.label}</button>
  {/each}
</div>

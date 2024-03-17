<script lang="ts">
  export let tags: { tag: string; color: string }[] = [];
</script>

<div class="flex flex-wrap gap-2">
  {#each tags as { tag, color }}
    <div class="flex items-center"> 
      <i class="mr-1 fa-solid fa-circle text-[14px] text-center" style="color: {color}" />
      <h1 class="text-[#ddd]">{tag}</h1>
    </div>
  {/each}
</div>

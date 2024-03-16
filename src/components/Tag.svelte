<script lang="ts">
  export let tags: { tag: string; color: string }[] = [];
</script>

<div class="flex flex-row space-x-2 tag">
  {#each tags as { tag, color }}
    <h1 class="text-[#ddd]">
      <i class="fa-solid fa-circle text-[14px] text-center" style="color: {color}" /> {tag}
    </h1>
  {/each}
</div>

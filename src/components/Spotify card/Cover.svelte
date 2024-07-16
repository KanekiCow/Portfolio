<script lang="ts">
  export let text: string;
</script>

<img
  class="object-fill w-full rounded-md thingy z-[-2]"
  alt="thing"
  src={text}
/>

<style>
  .thingy {
    box-shadow: inset 0px 0px 10px rgba(0, 0, 0, 0.9);
    transform: translateZ(15px);
  }
</style>

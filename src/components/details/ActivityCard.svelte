<!-- ActivityCard.svelte -->
<script lang="ts">
  import type {ActivityInfo} from "../../routes/+page.svelte"
  export let activityData:ActivityInfo;
</script>

<div class="bg-black/65 backdrop-blur-lg w-[1wv] rounded-lg border-[0px] border-[#797979]/80 p-[10px] flex flex-row mb-2">
  <img src={"https://dcdn.dstn.to/app-icons/" + activityData.application_id} alt="" class="h-[80px] w-[80px] rounded-lg bg-gradient-to-r from-[#1e1e1e] to-slate-900 border-[2px] animate-pulse shadow-pulse border-[#764ADE]" />
  <div class="flex flex-col ml-[10px]">
    <h1 class="font-medium text-gray-500">Running</h1>
    <p class="font-semibold">{activityData.name}</p>
  </div>
</div>

<style>
  .shadow-pulse {
    animation: pulse 1.5s infinite;
  }

  @keyframes pulse {
    0% {
      box-shadow: 0 0 0 0 rgba(118, 74, 222, 0.7);
    }
    70% {
      box-shadow: 0 0 0 10px rgba(255, 0, 0, 0);
    }
    100% {
      box-shadow: 0 0 0 0 rgba(255, 0, 0, 0);
    }
  }
</style>

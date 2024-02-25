<!-- ActivityCard.svelte -->
<script lang="ts">
  export let activity: {
    application_id: string;
    id: string;
    state: string;
    name: string;
    assets: {
      large_image: string;
    };
  };
</script>

<div
  class="bg-black/65 backdrop-blur-lg w-[400px] rounded-lg border-[0px] border-[#797979]/80 p-[10px] flex flex-row"
>
  <img
    src={"https://dcdn.dstn.to/app-icons/" + activity.application_id}
    alt=""
    class="h-[80px] w-[80px] rounded-lg bg-gradient-to-r from-[#1e1e1e] to-slate-900"
  />
  <div class="flex flex-col ml-[10px]">
    <h1 class="font-medium text-gray-500">Running</h1>
    <p class="font-semibold">{activity.name}</p>
  </div>
</div>

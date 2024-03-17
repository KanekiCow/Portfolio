<script lang="ts">
  import type { LanyardData } from "../../routes/+page.svelte";
  import SpotifyCard from "./SpotifyCard.svelte";
  import ActivityCard from "./ActivityCard.svelte";

  export let data: LanyardData;
</script>

{#if data.spotify !== null}
  <SpotifyCard spotifyData={data.spotify} />
{:else}
  <div
    class="flex flex-row mt-[10px] bg-black/65 backdrop-blur-lg w-[5wv] rounded-lg border-[0px] border-[#797979]/80 p-[10px] items-center"
  >
    <div
      class="h-[80px] w-[80px] rounded-lg bg-gradient-to-r from-[#1e1e1e] to-slate-900"
    />
    <div class="flex flex-col ml-[10px] justify-center">
      <h1 class="text-gray-500 font-medium">No Song Detected.</h1>
    </div>
  </div>
{/if}

<!-- Render other activity cards -->
{#if data.activities["1"] !== undefined && data.activities["1"].state != "custom" && data.activities?.["1"].name !== "Spotify"}
  <ActivityCard activityData={data.activities["1"]} />
{:else if data.activities["0"] != undefined && data.activities?.["1"] == undefined && data.activities["0"].state == undefined}
  <ActivityCard activityData={data.activities["0"]} />
{:else if data.activities["2"] !== undefined && data.activities["1"] !== undefined && data.activities["1"].name == "Spotify"}
  <ActivityCard activityData={data.activities["2"]} />
{:else}
  <!-- Handle other cases -->
{/if}

<!-- SpotifyCard.svelte -->
<script lang="ts">
    import type {SpotifyInfo} from "../../routes/+page.svelte"
  export let spotifyData: SpotifyInfo;
</script>

<div class="flex flex-row mt-[10px] bg-black/65 backdrop-blur-lg w-[1wv] rounded-lg border-[0px] border-[#797979]/80 p-[10px] items-center mb-2">
  <img src={spotifyData.album_art_url} alt="album" class="h-[80px] w-[80px] rounded-lg border-[2px] animate-pulse shadow-pulse border-[#764ADE]" />
  <div class="flex flex-col ml-[10px] truncate">
    <h1 class="text-[#764ADE] font-medium">Listening On Spotify</h1>
    <a href={"https://open.spotify.com/track/" + spotifyData.track_id} class="font-semibold">{spotifyData.song}</a>
    <h1 class="text-gray-400 font-semibold text-[14px]">{"By: " + spotifyData.artist}</h1>
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

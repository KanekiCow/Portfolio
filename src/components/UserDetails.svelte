<script lang="ts">
  import {Motion} from "svelte-motion"
  import type { LanyardData } from "../routes/+page.svelte"
   export let data: LanyardData;
   function copy() {
    if (data != undefined)
      return navigator.clipboard.writeText(data.discord_user.username);
  }
 
</script>
 <h1 class="ml-[20px] text-[#764ADE] roboto-regular"> <i class="fa-solid fa-caret-down overflow-hidden hover:rotate-[360deg] transition-all"/> ACTIVITIES</h1>
<div class="flex flex-row items-center mb-[20px] bg-black/40 p-3 rounded-lg  mt-[20px]">
 
  <div class="flex flex-row items-center mb-[20px] bg-black/40 p-3 rounded-lg  mt-[20px]">
            <img
              src={"https://cdn.discordapp.com/avatars" +
                "/" +
                data.discord_user.id +
                "/" +
                data.discord_user.avatar +
                ".png"}
              alt="pfp"
              class="rounded-full h-[110px]"
            />
            <div class="flex flex-col ml-[20px]">
              <div class="flex flex-row items-center">
                <h1 class="mb-[1px] text-[30px] font-semibold text-[#cecece]">
                  {data.discord_user.global_name}
                </h1>
                <h1
                  class={data.discord_status === "online"
                    ? "glow text-center px-[7px] ml-[7px] text-green-600 bg-green-900/50 rounded-lg border-[1,5px] border-green-400 pb-[2px]"
                    : data.discord_status === "dnd"
                      ? "glow-red text-center px-[7px] ml-[7px] text-red-600 bg-red-900/50 rounded-lg border-[1,5px] border-red-400 pb-[2px]"
                      : data.discord_status === "idle"
                        ? "glow-amber text-center px-[7px] ml-[7px] text-amber-500 bg-amber-900/50 rounded-lg border-[1,5px] border-amber-400 pb-[2px]"
                        : "text-center px-[7px] ml-[7px] text-gray-400 bg-gray-600/50 rounded-lg border-[1,5px] border-gray-400 pb-[2px]"}
                >
                  {data.discord_status === "online"
                    ? "Online"
                    : data.discord_status === "dnd"
                      ? "Busy"
                      : data.discord_status === "idle"
                        ? "Idle"
                        : "Offline"}
                </h1>
               
              </div>

              <div class="flex flex-row items-center">
                <span class="text-[#7b7b7b] mt-[1px]"
                  >{data.discord_user.username}</span
                >
                <button
                  on:click={copy}
                  class="active:scale-[.85] ease-linear transition-all duration-100 hover:text-[#999] ml-[5px] px-[10px] bg-slate-00/50 hover:bg-[#34343c]/50 rounded-[4px] text-[#7b7b7b]"
                  ><i class="fa-solid fa-copy"></i></button
                >
                
              </div>
              
              {#if data.activities?.["0"] !== undefined && data.activities?.["0"].name !== "Spotify" && data.activities["0"].state != undefined}
                <p>{data.activities["0"].state}</p>
              {:else if data.activities?.["0"] !== undefined && data.activities["0"].state == undefined}
                <p></p>
              {:else}
                <p></p>
              {/if}
            </div>
          </div>
</div>


<script lang="ts">
  import ActivityCard from "../components/ActivityCard.svelte";
  import { onMount, onDestroy } from "svelte";
  import Layout from "./__layout.svelte";
  import { Motion } from 'svelte-motion'
   interface DiscordUser {
    global_name: string;
    username: string;
    discriminator: string;
    avatar: string;
    id: string;
  }

  interface SpotifyInfo {
    track_id: string;
    song: string;
    artist: string;
    album_art_url: string;
  }

  interface LanyardData {
    discord_status: "online" | "dnd" | "idle";
    username: string;
    discord_user: DiscordUser;
    spotify: SpotifyInfo;
    activities: {
      "0": {
        application_id: string;
        id: string;
        state: string;
        name: string;
        assets: {
          large_image: string;
        };
      };

      "1": {
        application_id: string;
        id: string;
        state: string;
        name: string;
        assets: {
          large_image: string;
        };
      };

      "2": {
        application_id: string;
        id: string;
        state: string;
        name: string;
        assets: {
          large_image: string;
        };
      };
    };
  }

const item = {
 
    hidden: { y: 20, opacity: 0 },
    visible: { y: 0, opacity: 1 }
  
}

  let data: LanyardData | undefined;
  let loading = true;
  let vidRef: HTMLVideoElement;


  async function ManualFetch() {
    const ID = "1137623908263141426";

    try {
      const response = await fetch(`https://api.lanyard.rest/v1/users/${ID}`);
      if (!response.ok) {
        throw new Error("Failed to fetch data");
      }

      const { data: responseData } = await response.json();
      data = responseData;
      loading = false;
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  }

onMount(async () => {
  const ID = "1137623908263141426";

  function connectWebSocket() {
    try {
      const socket = new WebSocket('wss://api.lanyard.rest/socket');

      socket.addEventListener('open', async () => {
        // Send Opcode 2: Initialize after the connection is opened
        const initializePayload = JSON.stringify({
          op: 2,
          d: {
            subscribe_to_ids: [ID]
          }
        });
        socket.send(initializePayload);
      });

      socket.addEventListener('close', (event) => {
        console.log('WebSocket connection closed:', event.code, event.reason);
        console.log("Starting a new one asap ✅");
        // Automatically reconnect after a delay
        setTimeout(connectWebSocket, 1000); // Adjust delay as needed
      });

      socket.addEventListener('message', (event) => {
        const message = JSON.parse(event.data);

        if (message.op === 1) {
          // Handle Hello message (Opcode 1)
          // This message contains heartbeat_interval, but we're not using it in this example
        } else if (message.op === 0) {
          // Handle Event message (Opcode 0)
          if (message.t === 'INIT_STATE') {
            ManualFetch();
            // Here you can update your UI or perform other actions based on the received presence data
          } else if (message.t === 'PRESENCE_UPDATE') {
            // Handle PRESENCE_UPDATE event
            data = message.d;
            // Here you can update your UI or perform other actions based on the received presence update
          }
        }
      });

      socket.addEventListener('error', (error) => {
        console.error('WebSocket error:', error);
      });
    } catch (error) {
      console.error('Error with WebSocket:', error);
    }
  }

  connectWebSocket();
});

 
 

  onMount(() => {
  
    vidRef.muted = true;
  });
  function copy() {
    if (data != undefined)
      return navigator.clipboard.writeText(data.discord_user.username);
  }
 
</script>

<Layout>
  <div class="relative z-10 w-full flex justify-center items-center">
    <div
      class="bg-neutral-900/50 backdrop-blur-sm px-0 min-[795px]:w-[60%] min-[795px]:px-[50px] w-[98%] h-[100vh] overflow-hidden"
    >
      {#if loading}
        <p>Fetching...</p>
      {:else if data && data.discord_user}
        <div >
          <div class="flex flex-row items-center mb-[20px] mt-[20px] bg-black/40 p-3 rounded-lg">
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
          <div class="flex flex-row items-center mt-[5px] bg-black/40 p-[3px] rounded-lg">
            <div class=""> <Motion let:motion variants={item} initial={{y: 20, opacity: 0, filter: "blur(10px)"}} animate={{y: 0, opacity: 1, filter: "blur(0px)"}}>
            </Motion>
            <button class=" p-[5px] px-[10px] bg-black/40 rounded-lg active:scale-[.85] ease-linear transition-all duration-100 hover:bg-red-600/40"><i class="fa-solid fa-star mr-[5px] text-red-500"></i>Activities</button>
            <button class="ml-[5px] p-[5px] px-[10px] bg-black/40 rounded-lg active:scale-[.85] ease-linear transition-all duration-100 hover:bg-green-600/40"><i class="fa-brands fa-readme mr-[5px] text-green-500"></i>About</button>
            <button class="ml-[5px] p-[5px] px-[10px] bg-black/40 rounded-lg active:scale-[.85] ease-linear transition-all duration-100 hover:bg-blue-600/40"><i class="fa-solid fa-folder mr-[5px] text-blue-500"></i>Projects</button>
          </div>
          </div>
          {#if data.spotify !== null}
            <div
              class="flex flex-row mt-[10px] bg-black/65 backdrop-blur-lg w-[400px] rounded-lg border-[0px] border-[#797979]/80 p-[10px] items-center"
            >
              <img
                src={data.spotify.album_art_url}
                alt="album"
                class="h-[80px] w-[80px] rounded-lg border-[2px] animate-pulse shadow-pulse border-green-400"
              />
              <div class="flex flex-col ml-[10px] truncate">
                <h1 class="text-green-400 font-medium">Listening On Spotify</h1>
                <a
                  href={"https://open.spotify.com/track/" +
                    data.spotify.track_id}
                  class="font-semibold">{data.spotify.song}</a
                >
                <h1 class="text-gray-400 font-semibold text-[14px]">
                  {"By: " + data.spotify.artist}
                </h1>
              </div>
            </div>
          {:else}
            <div
              class="flex flex-row mt-[10px] bg-black/65 backdrop-blur-lg w-[400px] rounded-lg border-[0px] border-[#797979]/80 p-[10px] items-center"
            >
              <div
                class="h-[80px] w-[80px] rounded-lg bg-gradient-to-r from-[#1e1e1e] to-slate-900"
              />
              <div class="flex flex-col ml-[10px] justify-center">
                <h1 class="text-gray-500 font-medium">No Song Detected.</h1>
              </div>
            </div>
          {/if}
          <div class="flex flex-row mt-[10px]">
            {#if data.activities["1"] !== undefined && data.activities["1"].state != "custom" && data.activities?.["1"].name !== "Spotify"}
              <div
                class="bg-black/65 backdrop-blur-lg w-[400px] rounded-lg border-[0px] border-[#797979]/80 p-[10px] flex flex-row"
              >
                <img
                  src={"https://dcdn.dstn.to/app-icons/" +
                    data.activities["1"].application_id}
                  alt="                "
                  class="h-[80px] w-[80px] rounded-lg bg-gradient-to-r from-[#1e1e1e] to-slate-900"
                />
                <div class="flex flex-col ml-[10px]">
                  <h1 class="font-medium text-gray-500">Running</h1>
                  <p class="font-semibold">{data.activities["1"].name}</p>
                </div>
              </div>
            {:else if data.activities["0"] != undefined && data.activities?.["1"] == undefined && data.activities["0"].state == undefined}
              <div
                class="bg-black/65 backdrop-blur-lg w-[400px] rounded-lg border-[0px] border-[#797979]/80 p-[10px] flex flex-row"
              >
                <img
                  src={"https://dcdn.dstn.to/app-icons/" +
                    data.activities["0"].application_id}
                  alt="         "
                  class="h-[80px] w-[80px] rounded-lg bg-gradient-to-r from-[#1e1e1e] to-slate-900"
                />
                <div class="flex flex-col ml-[10px]">
                  <h1 class="font-medium text-gray-500">Running</h1>
                  <p class="font-semibold">{data.activities["0"].name}</p>
                </div>
              </div>
            {:else if data.activities["2"] !== undefined && data.activities["1"] !== undefined && data.activities["1"].name == "Spotify"}
              <div
                class="bg-black/65 backdrop-blur-lg w-[400px] rounded-lg border-[0px] border-[#797979]/80 p-[10px] flex flex-row"
              >
                <img
                  src={"https://dcdn.dstn.to/app-icons/" +
                    data.activities["2"].application_id}
                  alt="                "
                  class="h-[80px] w-[80px] rounded-lg bg-gradient-to-r from-[#1e1e1e] to-slate-900"
                />
                <div class="flex flex-col ml-[10px]">
                  <h1 class="font-medium text-gray-500">Running</h1>
                  <p class="font-semibold">{data.activities["2"].name}</p>
                </div>
              </div>
            {:else}
              <p></p>
            {/if}
          </div>
        </div>
      {:else}
        <p>Failed to fetch data</p>
      {/if}
    </div>
  </div>

  <div
    class="fixed top-0 left-0 w-full h-full -z-0 opacity-90 flex justify-center items-center"
  >
    <img class="fixed w-auto min-w-full min-h-full max-w-none blur-md object-contain" alt="bg" src="https://cdn.discordapp.com/attachments/1183485427596939294/1211408751026905088/571613_qwertfx_attempt-at-pixel-art-745813473.gif?ex=65ee1751&is=65dba251&hm=afe9b7c1816b17376bf48f13ba1d2ccac065c3781b0c05bb739eb3ca46c77889&"/>

  </div>
</Layout>

<style>

  .shadow-pulse {
    animation: pulse 1.5s infinite;
  }

  @keyframes pulse {
    0% {
      box-shadow: 0 0 0 0 rgba(74, 222, 128, 0.7);
    }
    70% {
      box-shadow: 0 0 0 10px rgba(255, 0, 0, 0);
    }
    100% {
      box-shadow: 0 0 0 0 rgba(255, 0, 0, 0);
    }
  }
</style>

<script lang="ts" >
  import { onMount } from "svelte";
  import UserDetails from "../components/UserDetails.svelte"
  import Layout from "./__layout.svelte";
  import ActivityButtons from "../components/ActivityButtons.svelte"
  import Cards from "../components/Cards.svelte"
 
  let data: LanyardData | undefined;
  let loading = true;

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

 
 

  
  
</script>
<script context="module" lang="ts">

    interface DiscordUser {
    global_name: string;
    username: string;
    discriminator: string;
    avatar: string;
    id: string;
  }
   export interface LanyardData {
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

 export interface SpotifyInfo {
    track_id: string;
    song: string;
    artist: string;
    album_art_url: string;
  }

export interface ActivityInfo {
    application_id: string;
    id: string;
    state: string;
    name: string;
    assets: {
      large_image: string;
    };
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
        <div class="flex flex-row items-center mt-[5px] bg-black/40 p-[5px] rounded-lg justify-center ">
            <div class="space-x-3">
              <ActivityButtons/>
          </div>
          </div>
        <div class="p-5 bg-black/30 mt-[20px] rounded-lg">
         <UserDetails {data} />
         <Cards {data}/>
         

         
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

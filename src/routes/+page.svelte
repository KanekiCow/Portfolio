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

<script lang="ts">
  import About from "../components/About.svelte";
  import { onMount } from "svelte";
  import UserDetails from "../components/UserDetails.svelte";
  import Layout from "./+layout.svelte";
  import ActivityButtons from "../components/ActivityButtons.svelte";
  import Cards from "../components/Cards.svelte";
  import { Motion } from "svelte-motion";

  const item = {
    hidden: { y: 20, opacity: 0 },
    visible: { y: 0, opacity: 1 },
  };
  let data: LanyardData | undefined;
  let loading = true;

  async function ManualFetch() {
    const ID = "1137623908263141426";

    try {
      const response = await fetch(`https://api.lanyard.rest/v1/users/${ID}`);
      if (!response.ok) {
        throw new Error("Failed to fetch data 😭");
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
        const socket = new WebSocket("wss://api.lanyard.rest/socket");

        socket.addEventListener("open", async () => {
            // Send Opcode 2: Initialize after the connection is opened
            const initializePayload = JSON.stringify({
                op: 2,
                d: {
                    subscribe_to_ids: [ID],
                },
            });
            socket.send(initializePayload);
        });

        socket.addEventListener("close", (event) => {
            console.log("WebSocket connection closed:", event.code, event.reason);
            console.log("Reconnecting my ass...");
            setTimeout(connectWebSocket, 1000);
        });

        socket.addEventListener("message", (event) => {
            const message = JSON.parse(event.data);

            if (message.op === 1) {
                
            } else if (message.op === 0) {
               
                if (message.t === "INIT_STATE") {
                    ManualFetch();
                   
                } else if (message.t === "PRESENCE_UPDATE") {
                  
                    data = message.d;
                  
                }
            }
        });

        socket.addEventListener("error", (error) => {
            console.error("WebSocket error:", error);
            console.log("Reconnecting...");
            // Automatically reconnect after a delay
            setTimeout(connectWebSocket, 1000);
        });
    } catch (error) {
        console.error("Error with WebSocket:", error);
    }
}

connectWebSocket();
});

  import { writable } from "svelte/store";

  let activeTab = writable("Activities");

  function setActiveTab(tab: string) {
    activeTab.set(tab);
  }
</script>

<Layout>
  <div class="relative z-10 w-full flex justify-center items-center">
    <div
      class="bg-neutral-900/50 backdrop-blur-sm px-0 min-[795px]:w-[60%] min-[795px]:px-[50px] w-[98%] h-[100vh] overflow-hidden"
    >
      {#if loading}
        <Motion
          let:motion
          variants={item}
          initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
          animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
          transition={{ delay: 0.2 }}
        >
          <div
            use:motion
            class="flex flex-row items-center mt-[15px] bg-black/40 p-[5px] rounded-lg justify-center h-[44px]"
          ></div>
        </Motion>
        <p>Fetching...</p>
      {:else if data && data.discord_user}
        <div
          class="flex flex-row items-center mt-[15px] bg-black/40 p-[5px] rounded-lg justify-center"
        >
          <div class="space-x-3 ">
            <ActivityButtons activeTab={$activeTab} {setActiveTab} />
          </div>
        </div>

       
        <div>
          {#if $activeTab === "Activities"}
            <Motion
              let:motion
              variants={item}
              initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
              animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
              transition={{ delay: 0.2 }}
            >
              <div use:motion class="p-5 bg-black/30 mt-[20px] rounded-lg">
                <Motion
                  let:motion
                  variants={item}
                  initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
                  animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
                  transition={{ delay: 0.3 }}
                >
                  <div use:motion>
                    <UserDetails {data} />
                  </div>
                </Motion>
                <Cards {data} />
              </div>
            </Motion>
            {:else if $activeTab === "About"}
            <About/>
          {/if}
        </div>

        
      {:else}
        <p>Failed to fetch data</p>
      {/if}
    </div>
  </div>

  <div
    class="fixed top-0 left-0 w-full h-full -z-0 opacity-90 flex justify-center items-center"
  >
    <img
      class="fixed w-auto min-w-full min-h-full max-w-none blur-md object-contain"
      alt="bg"
      src=""
    />
  </div>
</Layout>

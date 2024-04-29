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
  import Projects from "../components/pages/Projects.svelte"
    import Contacts from "../components/pages/Contacts.svelte"
  import About from "../components/pages/About.svelte";
  import { onMount } from "svelte";
  import UserDetails from "../components/pages/UserDetails.svelte";
  import Layout from "./+layout.svelte";
  import ActivityButtons from "../components/header/ActivityButtons.svelte";
  import Cards from "../components/details/Cards.svelte";
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
      class="bg-neutral-900/50 backdrop-blur-md px-0 min-[795px]:w-[60%] min-[795px]:px-[50px] w-[98%] h-[100vh] overflow-auto"
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
            class="flex flex-row items-center mt-[15px] bg-black/40 p-[5px] rounded-lg justify-center h-[44px] "
          ></div>
        </Motion>
        <p>Fetching...</p>
      {:else if data && data.discord_user}
        <div
          class="flex flex-row items-center mt-[15px] bg-black/40 p-[5px] rounded-lg justify-center "
        >
          <div class="space-x-3">
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
              <div use:motion class="p-5 bg-black/30 mt-[20px] rounded-lg ">
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
            <About />
            {:else if $activeTab === "Projects"}
            <Projects/>
               {:else if $activeTab === "Contacts"}
            <Contacts/>
          {/if}
        </div>
      {:else}
        <p>Failed to fetch data</p>
      {/if}
    </div>
  </div>

  <div
    class="fixed top-0 left-0 w-full h-full -z-0 opacity-90 flex justify-center items-center "
  >
  <svg class="fixed object-contain">
     
  <filter id='noiseFilter'>
    <feTurbulence 
      type='fractalNoise' 
      baseFrequency='0.6' 
      stitchTiles='stitch'/>
     <feColorMatrix in="colorNoise" type="matrix" values="1 0 0 0 0 0 1 0 0 0 0 0 1 0 0 0 0 0 1 0" />
        <feComposite operator="in" in2="SourceGraphic" result="monoNoise"/>
        <feBlend in="SourceGraphic" in2="monoNoise" mode="screen" />
  </filter>
  
</svg>
    <svg
      class="fixed w-auto min-w-full min-h-full max-w-none blur-md object-contain animate-rotate slow-rotation"
      width="585"
      height="475"
      viewBox="0 0 585 475"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <style>
        @keyframes colorChange1 {
          0%,
          100% {
            fill: var(--color1);
          }
          50% {
            fill: var(--color2);
          }
        }

        path {
          animation: colorChange1 8s infinite linear;
        }
      </style>
      <path
        d="M59.6878 70.4072C2.64247 112.7 -16.8108 220.14 15.7866 303.15C34.714 338.439 85.6079 417.473 137.764 451.308C202.958 493.601 346.492 482.305 380.666 392.728C414.841 303.151 608.848 251.138 582.56 142.122C556.271 33.1053 429.562 31.2664 323.621 6.83623C217.68 -17.5939 116.733 28.1141 59.6878 70.4072Z"
        fill="#B071FF"
      />
    </svg>
  </div>
</Layout>

<style>
  svg {
    filter: blur(100px);
  }
  :root {
    --color1: rgb(128, 61, 236);
    --color2: #ac38f0;
  }
  @keyframes rotate {
      from {
        transform: rotate(0deg);
      }
      to {
        transform: rotate(360deg);
      }
    }

    .slow-rotation {
      animation: rotate 10s cubic-bezier(0.4, 0, 0.2, 1) infinite; /* Adjust the duration to make it slower or faster */
    }
</style>

<script lang="ts">
  import { Motion } from "svelte-motion";
  import { onMount } from "svelte";
  import Typed from "typed.js";
  import SpotifyDetails from "../details/SpotifyDetails.svelte";

  let element: HTMLElement;
  let c: HTMLElement;

  const item = {
    hidden: { y: 20, opacity: 0 },
    visible: { y: 0, opacity: 1 },
  };

  onMount(() => {
    const typed = new Typed(element, {
      strings: ["./about.sh"],
      typeSpeed: 70,
      cursorChar: "▐"
    });
    const typed2 = new Typed(c, {
      strings: ["Hey there, I'm Kaneki Cat, passionate about bringing ideas to life. \n As a self-taught front-end web developer and UI/UX designer, I \n thrive on creating and seeing projects through. \n I've tackled diverse challenges both solo and with teams.\nMy toolkit includes: \n - LuaU for Roblox development \n - C# for .NET Windows Form and WPF apps \n - C++ \n - TypeScript/JavaScript \n - Firebase \n - Svelte \n - ReactJS \n - Tailwind CSS \n - HTML \n and I manage it all with Git, Yarn, and npm."],
      typeSpeed: 0.001,
      showCursor: false
    });

    // when unmounted
    return () => {
      typed.destroy();
      typed2.destroy();
    };
  });
</script>

<Motion
  let:motion
  variants={item}
  initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
  animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
  transition={{ delay: 0.1 }}
>
  <div class="p-5 bg-black/30 mt-[20px] rounded-lg ">
    <h1 class="ml-[20px] text-[#764ADE] roboto-regular">
      <i
        class="fa-solid fa-caret-down overflow-hidden hover:rotate-[360deg] transition-all"
      /> ABOUT
    </h1>
    <Motion
      let:motion
      initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
      animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
      transition={{ delay: 0.2 }}
    >
      <div
        use:motion
        class="flex flex-row items-center mb-[10px] bg-black/40 p-3 rounded-lg mt-[20px] border-2 border-gray-600/40 backdrop-blur-sm"
      >
        <i
          class="fa-solid fa-arrow-turn-up overflow-hidden rotate-[90deg] text-violet-400 transition-all mr-[10px]"
        /> <span bind:this={element} class="text-gray-400 jetbrain" />
      </div>
    </Motion>
    <Motion
      let:motion
      initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
      animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
      transition={{ delay: 1 }}
    >
      <div
        use:motion
        class="flex flex-row items-center mb-[20px] bg-black/40 p-3 rounded-lg border-2 border-gray-600/40 backdrop-blur-sm"
      >
        <span bind:this={c} class="text-gray-400  w-auto jetbrain" />
      </div>
    </Motion>
  </div>
</Motion>

<SpotifyDetails/>

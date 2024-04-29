<script lang="ts">
  import ProjectCards from "../projects/ProjectCards.svelte";
  import { Motion } from "svelte-motion";
  const item = {
    hidden: { y: 20, opacity: 0 },
    visible: { y: 0, opacity: 1 },
  };
</script>

<div class="p-5 bg-black/30 mt-[20px] rounded-lg">
  <h1 class="ml-[20px] text-[#764ADE] roboto-regular">
    <i
      class="fa-solid fa-caret-down overflow-hidden hover:rotate-[360deg] transition-all"
    /> PROJECT HIGHLIGHTS
  </h1>

  <div class="grid min-[1363px]:grid-cols-2 grid-cols-1 gap-1">
    <Motion
      let:motion
      variants={item}
      initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
      animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
      transition={{ delay: 0.2 }}
    >
      <div use:motion>
        <ProjectCards
          headerText="Portfolio"
          descriptionText="Simply My Portfolio to learn and know more about me"
          tags={[
            { text: "Svelte", color: "#ff5400" },
            { text: "Typescript", color: "#0087ff" },
            { text: "Tailwind", color: "#033abd" },
          ]}
          buttonLinks={[
            { label: "Source", url: "https://github.com/KanekiCow/Portfolio" },
            { label: "View", url: "https://example.com/view" },
          ]}
        />
      </div>
    </Motion>
    <Motion
      let:motion
      variants={item}
      initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
      animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
      transition={{ delay: 0.3 }}
    >
      <div use:motion>
        <ProjectCards
          headerText="The Lions Textile Industries"
          descriptionText="A simple front-end website made for a client of mine"
          tags={[
            { text: "Svelte", color: "#ff5400" },
            { text: "Astro", color: "rgb(213, 51, 51)" },
            { text: "Typescript", color: "#0087ff" },
            { text: "Tailwind", color: "#033abd" },
          ]}
          buttonLinks={[
            {
              label: "Source",
              url: "https://github.com/KanekiCow/The-Lions-Textile-Industries",
            },
            { label: "View", url: "https://testing-kanekicow.vercel.app" },
          ]}
        />
      </div>
    </Motion>
    <Motion
      let:motion
      variants={item}
      initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
      animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
      transition={{ delay: 0.4 }}
    >
      <div use:motion>
        <ProjectCards
          headerText="NekoGacha"
          descriptionText="A simple website made in 2021 for testing the cat API and firebase"
          tags={[
            { text: "React.js", color: "rgb(85, 71, 253)" },
            { text: "Css", color: "rgb(131, 80, 242)" },
            { text: "Typescript", color: "#0087ff" },
            { text: "Firebase", color: "rgb(240, 137, 45)" },
          ]}
          buttonLinks={[
            { label: "Source", url: "https://github.com/KanekiCow/NekoGacha" },
            { label: "View", url: "https://neko-gacha.vercel.app" },
          ]}
        />
      </div>
    </Motion>
    <Motion
      let:motion
      variants={item}
      initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
      animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
      transition={{ delay: 0.5 }}
    >
      <div use:motion>
        <ProjectCards
          headerText="Donehub"
          descriptionText="A simple website made in 2021 for testing firebase"
          tags={[
            { text: "React.js", color: "rgb(85, 71, 253)" },
            { text: "Css", color: "rgb(131, 80, 242)" },
            { text: "Typescript", color: "#0087ff" },
            { text: "Firebase", color: "rgb(240, 137, 45)" },
          ]}
          buttonLinks={[
            { label: "Source", url: "https://github.com/KanekiCow/NekoGacha" },
            { label: "View", url: "https://neko-gacha.vercel.app" },
          ]}
        />
      </div>
    </Motion>
    <Motion
      let:motion
      variants={item}
      initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
      animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
      transition={{ delay: 0.6 }}
    >
      <div use:motion>
        <ProjectCards
          headerText="Valiant Roblox Executor"
          descriptionText="Roblox scripting Utils, made in .Net WPF"
          tags={[
            { text: "C#", color: "rgb(71, 253, 82)" },
            { text: ".Net", color: "rgb(225, 41, 251)" },
          ]}
          buttonLinks={[
            {
              label: "Source",
              url: "https://github.com/KanekiCow/Valiant-Roblox-Executor",
            },
          ]}
        />
      </div>
    </Motion>

    <Motion
      let:motion
      variants={item}
      initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
      animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
      transition={{ delay: 0.7 }}
    >
      <div use:motion>
        <ProjectCards
          headerText="Seiryu Roblox Executor Website"
          descriptionText="A basic website made with HTML, Css and a bit of Js for a client."
          tags={[
            { text: "Css", color: "rgb(131, 80, 242)" },
            { text: "HTML", color: "rgb(247, 174, 2)" },
            { text: "JavaScript", color: "rgb(205, 247, 2)" },
          ]}
          buttonLinks={[
            { label: "Source", url: "https://github.com/KanekiCow/Seiryu" },
            { label: "View", url: "https://projectseiryu.vercel.app" },
          ]}
        />
      </div>
    </Motion>
  </div>
</div>

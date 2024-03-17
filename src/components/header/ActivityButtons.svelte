<script lang="ts">
  import { Motion } from "svelte-motion";
  import tabSwitchSound from "../../components/sound/button-124476.mp3";

  let hoverStates: { [key: string]: boolean } = {};
  let selectedTab: string; 
  let hoveredTab: string; 

  const tabSwitchSoundInstance = new Audio(tabSwitchSound);

  const handleMouseEnter = (tabName: string) => {
    hoverStates[tabName] = true;
    hoveredTab = tabName; 
    console.log(`${tabName} - Mouse entered`);
  };

  const handleMouseLeave = (tabName: string) => {
    hoverStates[tabName] = false;
    hoveredTab = '';
    console.log(`${tabName} - Mouse left`);
  };

  const variants = {
    open: { x: 0, opacity: 1, filter: "blur(0px)" },
    closed: { x: -20, opacity: 0, filter: "blur(0px)" },
  };

  const item = {
    hidden: { y: 20, opacity: 0 },
    visible: { y: 0, opacity: 1 },
  };

  export let activeTab = "Activities";
  export let setActiveTab: (tab: string) => void;

  const tabDetails = [
    { name: "Activities", icon: "fa-solid fa-rocket" },
    { name: "About", icon: "fa-solid fa-circle-user" },
    { name: "Projects", icon: "fa-solid fa-layer-group" },
    { name: "Contacts", icon: "fa-solid fa-envelope" },
     { name: "My gf", icon: "fa-solid fa-heart" },
  ];

  function changeTab(tab: string) {
    if (tab !== activeTab) {
      setActiveTab(tab);
      selectedTab = tab;
      tabSwitchSoundInstance.play();
    }
     
  }
</script>

<div class="space-x-3 flex flex-row">
  {#each tabDetails as tab, index}
    <Motion
      let:motion
      variants={item}
      initial={{ y: 20, opacity: 0, filter: "blur(10px)" }}
      animate={{ y: 0, opacity: 1, filter: "blur(0px)" }}
      transition={{ delay: index * 0.1 }}>
      <button
        use:motion
        on:mouseenter={() => handleMouseEnter(tab.name)}
        on:mouseleave={() => handleMouseLeave(tab.name)}
        class:selected={activeTab === tab.name}
        class:hovered={(hoveredTab === tab.name || activeTab === tab.name) && activeTab !== tab.name}
        on:click={() => changeTab(tab.name)}
        class="h-[34px] item p-[5px] px-[10px] rounded-lg active:scale-[.85] ease-linear transition-all duration-100 group/button flex flex-row justify-center items-center hover:px-4"
        style={`background-color: ${((hoveredTab === tab.name || activeTab === tab.name) && activeTab === tab.name) ? '#764ADE40' : '#0F172A66'}`}
      >
        <i
          class={`fa-solid ${tab.icon} mx-[5px] text-[#4d4d4d] transition-all group-hover/button:text-[#764ADE] ${(hoveredTab === tab.name || activeTab === tab.name) && activeTab === tab.name ? 'text-[#764ADE]' : ''}`}
        ></i>
        {#if hoverStates[tab.name] }
          <Motion
            let:motion
            {variants}
            initial={{ x: -20, opacity: 0, filter: "blur(10px)" }}
            animate={ activeTab === tab.name ? "open" : "open"}
            transition={{ duration: 0.1 }}
          >
            <h1 use:motion class="roboto-regular transition-all">
              {hoveredTab}
            </h1>
          </Motion>
        {:else}
          <span></span>
           {#if activeTab === tab.name} <h1 class="roboto-regular">{tab.name}</h1> 
          {/if}
        {/if}
      </button>
    </Motion>
  {/each}
</div>

<script lang="ts">
  import { Motion } from "svelte-motion";
  import Header from "./Header.svelte";
  import Description from "./Description.svelte";
  import ButtonLinks from "./ButtonLinks.svelte";
  import Tag from "./Tag.svelte";

  interface TagItem {
    text: string;
    color: string;
  }

  export let headerText: string = "";
  export let descriptionText: string = "";
  export let tags: TagItem[] = [];
  export let buttonLinks: { label: string; url: string }[] = [];
</script>

<div
  class="flex flex-col mb-[5px] bg-gradient-to-r from-black/40 to-black/50 bg- p-[14px] rounded-lg mt-[5px] border-2 border-gray-600/40 hover:from-black/50 hover:to-black/60 hover:border-black/10 transition-all hover:shadow-2xl hover:backdrop-blur-3xl overflow-auto"
>
  <Header text={headerText} />
  <Tag tags={tags.map((item) => ({ tag: item.text, color: item.color }))} />
  <Description text={descriptionText} />
  <ButtonLinks links={buttonLinks} />
</div>

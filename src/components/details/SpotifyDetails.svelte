<script lang="ts">
  import MainCard from "../Spotify card/MainCard.svelte";
  import { Motion } from "svelte-motion";
  const item = {
    hidden: { y: 20, opacity: 0, filter: "blur(10px)" },
    visible: { y: 0, opacity: 1, filter: "blur(0px)" },
  };
</script>

<div class="flex flex-col items-center">
  <h1 class="ml-[20px] text-[#764ADE] roboto-regular mb-5">
    COMFORT SONGS
  </h1>

  <div class="grid min-[1363px]:grid-cols-4 grid-cols-2 gap-3">
    <Motion
      let:motion
      variants={item}
      initial="hidden"
      animate="visible"
      transition={{ delay: 0.2 }}
    >
      <div use:motion>
        <MainCard
          title="True Love Waits"
          artist="Radiohead"
          cover="https://i.scdn.co/image/ab67616d00001e0245643f5cf119cbc9d2811c22"
        />
      </div>
    </Motion>

    <Motion
      let:motion
      variants={item}
      initial="hidden"
      animate="visible"
      transition={{ delay: 0.3 }}
    >
      <div use:motion>
        <MainCard
          title="A Quick One Before the Eternal Worm Devours Connecticut"
          artist="Have A Nice Life"
          cover="https://i.scdn.co/image/ab67616d00001e02a54f2b401501b3569990c256"
        />
      </div>
    </Motion>

    <Motion
      let:motion
      variants={item}
      initial="hidden"
      animate="visible"
      transition={{ delay: 0.4 }}
    >
      <div use:motion>
        <MainCard
          title="No Surprises"
          artist="Radiohead"
          cover="https://i.scdn.co/image/ab67616d00001e02c8b444df094279e70d0ed856"
        />
      </div>
    </Motion>

    <Motion
      let:motion
      variants={item}
      initial="hidden"
      animate="visible"
      transition={{ delay: 0.5 }}
    >
      <div use:motion>
        <MainCard
          title="Like You Do"
          artist="Joji"
          cover="https://i.scdn.co/image/ab67616d00001e02f733e50079838090eebc3fe4"
        />
      </div>
    </Motion>

    <Motion
      let:motion
      variants={item}
      initial="hidden"
      animate="visible"
      transition={{ delay: 0.6 }}
    >
      <div use:motion>
        <MainCard
          title="If I Stare At the Clock Long Enough, Will I Have the Time to Tell You Everything?"
          artist="dandelion hands"
          cover="https://i.scdn.co/image/ab67616d00001e021936dfa81ba2eb3113fc489f"
        />
      </div>
    </Motion>

    <Motion
      let:motion
      variants={item}
      initial="hidden"
      animate="visible"
      transition={{ delay: 0.7 }}
    >
      <div use:motion>
        <MainCard
          title="i'm going to fail my class"
          artist="mage tears"
          cover="https://i.scdn.co/image/ab67616d00001e02f562a796d7e1d0e203029d03"
        />
      </div>
    </Motion>

    <Motion
      let:motion
      variants={item}
      initial="hidden"
      animate="visible"
      transition={{ delay: 0.8 }}
    >
      <div use:motion>
        <MainCard
          title="Cry"
          artist="Cigarettes After Sex"
          cover="https://i.scdn.co/image/ab67616d00001e02fd275af89cec73d6287f9cbf"
        />
      </div>
    </Motion>

    <Motion
      let:motion
      variants={item}
      initial="hidden"
      animate="visible"
      transition={{ delay: 0.9 }}
    >
      <div use:motion>
        <MainCard
          title="Creep"
          artist="Radiohead"
          cover="https://i.scdn.co/image/ab67616d00001e02df55e326ed144ab4f5cecf95"
        />
      </div>
    </Motion>
  </div>

  <h1 class="ml-[20px] text-[#764ADE] roboto-regular mb-5 mt-[30px]">
    FAVORITE ARTISTS
  </h1>

  <div class="grid min-[1363px]:grid-cols-4 grid-cols-2 gap-3">
    <MainCard
      title="Radiohead"
      artist="Alternative Rock"
      cover="https://i.scdn.co/image/ab6761610000e5eba03696716c9ee605006047fd"
    />

    <MainCard
      title="Cigarettes After Sex"
      artist="Dream Pop"
      cover="https://i.scdn.co/image/ab6761610000e5eb674c5dace43fe2e2645d314b"
    />

    <MainCard
      title="Mac DeMarco"
      artist="Indie Rock"
      cover="https://i.scdn.co/image/ab6761610000e5eb3cef7752073cbbd2cc04c6f0"
    />

    <MainCard
      title="dandelion hands"
      artist="Emo Lo-fi"
      cover="https://i.scdn.co/image/ab6761610000e5eb2be8958db3ec0b735f6e57a0"
    />

    <MainCard
      title="sign crushes motorist"
      artist="Indie Pop"
      cover="https://i.scdn.co/image/ab67616d00001e029ff5156f825ae0e06e15ff46"
    />

    <MainCard
      title="Have A Nice Life"
      artist="Shoegaze"
      cover="https://i.scdn.co/image/ab67616d00001e02a54f2b401501b3569990c256"
    />

    <MainCard
      title="Pierce The Veil"
      artist="Post-Hardcore"
      cover="https://i.scdn.co/image/ab6761610000e5ebc9461fa3257fbddc14c33202"
    />

    <MainCard
      title="Foo Fighters"
      artist="Alternative Rock"
      cover="https://i.scdn.co/image/ab6761610000e5ebc884df599abc793c116cdf15"
    />
  </div>
</div>

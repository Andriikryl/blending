<script lang="ts">
  import { GUI, guiControls } from "./index";
  const gui = guiControls({
    Background_color: "#0ea5e9",
    Foreground_color: "#f43f5e",
  });
  const blendMods = [
    {
      title: "Normal",
      blend: "mix-blend-mode: normal;",
    },
    {
      title: "Multiply",
      blend: "mix-blend-mode: multiply;",
    },
    {
      title: "screen",
      blend: "mix-blend-mode: screen;",
    },
    {
      title: "overlay",
      blend: "mix-blend-mode: overlay;",
    },
    {
      title: "Darken",
      blend: "mix-blend-mode: darken;",
    },
    {
      title: "lighten",
      blend: "mix-blend-mode: lighten;",
    },
    {
      title: " color-dodge",
      blend: "mix-blend-mode: color-dodge;",
    },
    {
      title: " color-burn",
      blend: "mix-blend-mode: color-burn;",
    },
    {
      title: "hard-light",
      blend: "mix-blend-mode: hard-light;",
    },
    {
      title: "difference",
      blend: "mix-blend-mode: difference;",
    },
    {
      title: "exclusion",
      blend: "mix-blend-mode: exclusion;",
    },
    {
      title: "hue",
      blend: "mix-blend-mode: hue;",
    },
    {
      title: "saturation",
      blend: "mix-blend-mode: saturation;",
    },
    {
      title: "luminosity",
      blend: "mix-blend-mode: luminosity;",
    },
    {
      title: " plus-darker",
      blend: "mix-blend-mode: plus-darker;",
    },
    {
      title: "plus-lighter",
      blend: "mix-blend-mode: plus-lighter;",
    },
  ];
</script>

<div>
  <div class="container">
    <GUI controls={gui} />
  </div>
  <div class="blend__group">
    {#each blendMods as blend}
      <div class="wrapper">
        <div
          class="box"
          style="background-color: {$gui.Background_color};"
        ></div>
        <div
          class="boxBg"
          style="background-color: {$gui.Foreground_color}; {blend.blend}"
        ></div>
      </div>
    {/each}
  </div>
</div>

<style>
  .container {
    width: max-content;
    margin-inline: auto;
    margin-block-end: 50px;
  }
  .blend__group {
    --layout-grid-min: 30ch;
    --layout-grid-gap: 4vw;
    display: grid;
    place-items: center;
    grid-template-columns: repeat(
      auto-fit,
      minmax(min(100%, var(--layout-grid-min)), 1fr)
    );
    gap: var(--layout-grid-gap);
    margin-block-end: 50px;
  }
  .wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .box {
    width: 100px;
    height: 100px;
  }
  .boxBg {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    position: relative;
    left: -54px;
    bottom: -40px;
    z-index: 10;
  }
</style>

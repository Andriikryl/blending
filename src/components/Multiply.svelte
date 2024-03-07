<script lang="ts">
  import BlandDescription from "./BlandDescription.svelte";
  import BlandExemple from "./BlandExemple.svelte";
  import BlandTitle from "./BlandTitle.svelte";
  import BoxSeparetor from "./BoxSeparetor.svelte";
  import FinalBackdrop from "./FinalBackdrop.svelte";
  import SpeechBubble from "./SpeechBubble.svelte";
  import { GUI, guiControls } from "./index";
  const gui = guiControls({
    R: 244,
    G: 63,
    B: 94,
  });
  const guiBg = guiControls({
    R: 14,
    G: 165,
    B: 233,
  });
  let minR: string;
  let minG: string;
  let minB: string;
  let bkR: number;
  let bkG: number;
  let bkB: number;
  $: {
    minR = (($gui.R / 255) * ($guiBg.R / 255)).toFixed(2);
    minG = (($gui.G / 255) * ($guiBg.G / 255)).toFixed(2);
    minB = (($gui.B / 255) * ($guiBg.B / 255)).toFixed(2);
    bkR = parseFloat(minR) * 255;
    bkG = parseFloat(minG) * 255;
    bkB = parseFloat(minB) * 255;
  }
  $: algoritmsData = [
    "multiplies each channel together.",
    `Blend ---> background-color: rgb(${$gui.R}, ${$gui.G}, ${$gui.B})`,
    `Background ---> background-color: rgb(${$guiBg.R}, ${$guiBg.G}, ${$guiBg.B})`,
    `Result ---> background-color: rgb(${minR}, ${minG}, ${minB})`,
  ];
</script>

<div class="wrapper">
  <BlandTitle tag="h3">Multiply</BlandTitle>
  <SpeechBubble>B(Cb, Cs) = Cb x Cs</SpeechBubble>
  <BlandDescription>Multiplies each channel together..</BlandDescription>
  <BoxSeparetor>
    <svelte:fragment slot="item-start">
      <div class="control__bg">
        <GUI controls={gui} />
      </div>
      <div class="control__main">
        <GUI controls={guiBg} />
      </div>
    </svelte:fragment>
    <svelte:fragment slot="item-end">
      <BlandDescription>Backdrop values numbers</BlandDescription>
      <div class="flex__group">
        <div
          class="iiner__box"
          style="background-color: rgb({+minR * 255}, 0, 0);"
        >
          <p class="inner__title">{minR}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, {+minG * 255}, 0);"
        >
          <p class="inner__title">{minG}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, 0, {+minB * 255});"
        >
          <p class="inner__title">{minB}</p>
        </div>
      </div>
    </svelte:fragment>
  </BoxSeparetor>
  <BlandExemple {gui} {guiBg} blendmode="mix-blend-mode: multiply;" />
  <div class="backdrop__wrapper">
    <FinalBackdrop {bkB} {bkG} {bkR} />
    <div>
      <BlandDescription>Algorithm</BlandDescription>
      <ol class="algoritms__list">
        {#each algoritmsData as algoritm}
          <li>{algoritm}</li>
        {/each}
      </ol>
    </div>
  </div>
</div>

<style>
  .wrapper {
    margin-block-end: 20px;
  }
  .flex__group {
    display: flex;
    gap: 10px;
    margin-block-start: 10px;
  }
  .control__bg {
    display: flex;
    gap: 10px;
    align-items: center;
  }
  .control__main {
    display: flex;
    gap: 10px;
    align-items: center;
  }
  .control__bg::before {
    content: "";
    display: block;
    width: 40px;
    height: 40px;
    background-color: rgb(244, 63, 94);
    border-radius: 50%;
    position: relative;
    bottom: 10px;
  }
  .control__main::before {
    content: "";
    display: block;
    width: 40px;
    height: 40px;
    background-color: rgb(14, 165, 233);
    position: relative;
    bottom: 10px;
  }
  .iiner__box {
    --size: 90px;
    width: var(--size);
    height: var(--size);
    display: grid;
    place-items: center;
  }
  .inner__title {
    color: #fff;
  }
</style>

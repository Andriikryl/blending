<script lang="ts">
  import Decimal from "decimal.js";
  import BlandDescription from "./BlandDescription.svelte";
  import BlandExemple from "./BlandExemple.svelte";
  import BlandTitle from "./BlandTitle.svelte";
  import BoxSeparetor from "./BoxSeparetor.svelte";
  import SpeechBubble from "./SpeechBubble.svelte";

  import { GUI, guiControls } from "./index";
  import FinalBackdrop from "./FinalBackdrop.svelte";
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

  let normolizeBgR: number;
  let normolizeBgG: number;
  let normolizeBgB: number;
  let invertBgrR: number;
  let invertBgrG: number;
  let invertBgrB: number;
  let normilizeFoR: number;
  let normilizeFoG: number;
  let normilizeFoB: number;
  let devideR: number;
  let devideG: number;
  let devideB: number;
  let ivertResultR: number;
  let ivertResultG: number;
  let ivertResultB: number;
  let finalColorBgR: number;
  let finalColorBgG: number;
  let finalColorBgB: number;
  function clamp(value: number, min = 0, max = 1) {
    return Math.min(Math.max(value, min), max);
  }
  $: {
    normolizeBgR = $guiBg.R / 255;
    normolizeBgG = $guiBg.G / 255;
    normolizeBgB = $guiBg.B / 255;
  }
  $: {
    normilizeFoR = $gui.R / 255;
    normilizeFoG = $gui.G / 255;
    normilizeFoB = $gui.B / 255;
  }
  $: {
    invertBgrR = 1 - normolizeBgR;
    invertBgrG = 1 - normolizeBgG;
    invertBgrB = 1 - normolizeBgB;
  }
  $: {
    devideR = clamp(invertBgrR / normilizeFoR);
    devideG = clamp(invertBgrG / normilizeFoG);
    devideB = clamp(invertBgrB / normilizeFoB);
  }
  $: {
    ivertResultR = clamp(Math.abs(1 - devideR));
    ivertResultG = clamp(Math.abs(1 - devideG));
    ivertResultB = clamp(Math.abs(1 - devideB));
  }
  $: {
    finalColorBgR = Math.floor(ivertResultR * 255);
    finalColorBgG = Math.floor(ivertResultG * 255);
    finalColorBgB = Math.floor(ivertResultB * 255);
  }
  $: algoritmsData = [
    "normalise the values between 0 and 1 to work this out",
    `invert the bg`,
    `divide it by the foreground`,
    `invert the result`,
    `Result ---> background-color: rgb(${finalColorBgR}, ${finalColorBgG}, ${finalColorBgB})`,
  ];
</script>

<div class="wrapper">
  <BlandTitle tag="h3">Color Burn</BlandTitle>
  <SpeechBubble
    >if(Cb == 1) B(Cb, Cs) = 1 else if(Cs == 0) B(Cb, Cs) = 0 else B(Cb, Cs) = 1
    - min(1, (1 - Cb) / Cs)</SpeechBubble
  >
  <BlandDescription
    >Darkens the backdrop color to reflect the source color. Painting with white
    produces no change.</BlandDescription
  >
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
          style="background-color: rgb({finalColorBgR}, 0, 0);"
        >
          <p class="inner__title">{ivertResultR.toFixed(2)}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, {finalColorBgG}, 0);"
        >
          <p class="inner__title">{ivertResultG.toFixed(2)}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, 0, {finalColorBgB});"
        >
          <p class="inner__title">{ivertResultB.toFixed(2)}</p>
        </div>
      </div>
    </svelte:fragment>
  </BoxSeparetor>
  <BlandExemple {gui} {guiBg} blendmode="mix-blend-mode: color-burn;" />
  <div class="backdrop__wrapper">
    <FinalBackdrop
      bkB={finalColorBgB}
      bkG={finalColorBgG}
      bkR={finalColorBgR}
    />
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
    margin-block-end: 60px;
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

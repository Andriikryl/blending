<script lang="ts">
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
  let normilizeFoR: number;
  let normilizeFoG: number;
  let normilizeFoB: number;
  let SumBgR: number;
  let SumBgG: number;
  let SumBgB: number;
  let MultBgR: number;
  let MultBgG: number;
  let MultBgB: number;
  let subtrBgR: number;
  let subtrBgG: number;
  let subtrBgB: number;
  let convetrFinalR: number;
  let convetrFinalG: number;
  let convetrFinalB: number;
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
    SumBgR = normilizeFoR + normolizeBgR;
    SumBgG = normilizeFoG + normolizeBgG;
    SumBgB = normilizeFoB + normolizeBgB;
  }
  $: {
    MultBgR = normilizeFoR * normolizeBgR * 2;
    MultBgG = normilizeFoG * normolizeBgG * 2;
    MultBgB = normilizeFoB * normolizeBgB * 2;
  }
  $: {
    subtrBgR = +(SumBgR - MultBgR).toFixed(2);
    subtrBgG = +(SumBgG - MultBgG).toFixed(2);
    subtrBgB = +(SumBgB - MultBgB).toFixed(2);
  }
  $: {
    convetrFinalR = Math.floor(subtrBgR * 255);
    convetrFinalG = Math.floor(subtrBgG * 255);
    convetrFinalB = Math.floor(subtrBgB * 255);
  }

  $: algoritmsData = [
    "normalise the values between 0 and 1 to work this out",
    `sum each channel`,
    `Multiply the product of each by 2`,
    `Subtract 2 from 1`,
    `Result ---> background-color: rgb(${convetrFinalR}, ${convetrFinalG}, ${convetrFinalB})`,
  ];
</script>

<div class="wrapper">
  <BlandTitle tag="h3">Exclusion</BlandTitle>
  <SpeechBubble>B(Cb, Cs) = Cb + Cs - 2 x Cb x Cs</SpeechBubble>
  <BlandDescription
    >Produces an effect similar to that of the Difference mode but lower in
    contrast. Painting with white inverts the backdrop color; painting with
    black produces no change</BlandDescription
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
          style="background-color: rgb({convetrFinalR}, 0, 0);"
        >
          <p class="inner__title">{subtrBgR}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, {convetrFinalG}, 0);"
        >
          <p class="inner__title">{subtrBgG}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, 0, {convetrFinalB});"
        >
          <p class="inner__title">{subtrBgB}</p>
        </div>
      </div>
    </svelte:fragment>
  </BoxSeparetor>
  <BlandExemple {gui} {guiBg} blendmode="mix-blend-mode: exclusion;" />
  <div class="backdrop__wrapper">
    <FinalBackdrop
      bkB={convetrFinalB}
      bkG={convetrFinalG}
      bkR={convetrFinalR}
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

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
    minR = ((1 - $gui.R / 255) * (1 - $guiBg.R / 255)).toFixed(2);
    minG = ((1 - $gui.G / 255) * (1 - $guiBg.G / 255)).toFixed(2);
    minB = ((1 - $gui.B / 255) * (1 - $guiBg.B / 255)).toFixed(2);
  }
  $: invertR = 1 - +minR;
  $: invertG = 1 - +minG;
  $: invertB = 1 - +minB;
  $: {
    bkR = +(invertR * 255).toFixed(2);
    bkG = +(invertG * 255).toFixed(2);
    bkB = +(invertB * 255).toFixed(2);
  }
</script>

<div class="wrapper">
  <BlandTitle tag="h3">Screen</BlandTitle>
  <SpeechBubble
    >B(Cb, Cs) = 1 - [(1 - Cb) x (1 - Cs)] = Cb + Cs -(Cb x Cs)</SpeechBubble
  >
  <BlandDescription
    >Inverts both the inputs and the result, which is why the result is always
    lighter.</BlandDescription
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
          style="background-color: rgb({+minR * 255}, 0, 0);"
        >
          <p class="inner__title">{invertR.toFixed(2)}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, {+minG * 255}, 0);"
        >
          <p class="inner__title">{invertG.toFixed(2)}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, 0, {+minB * 255});"
        >
          <p class="inner__title">{invertB.toFixed(2)}</p>
        </div>
      </div>
    </svelte:fragment>
  </BoxSeparetor>
  <BlandExemple {gui} {guiBg} blendmode="mix-blend-mode: screen;" />
  <FinalBackdrop {bkB} {bkG} {bkR} />
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

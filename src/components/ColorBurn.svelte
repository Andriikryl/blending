<script lang="ts">
  import BlandDescription from "./BlandDescription.svelte";
  import BlandExemple from "./BlandExemple.svelte";
  import BlandTitle from "./BlandTitle.svelte";
  import BoxSeparetor from "./BoxSeparetor.svelte";
  import FinalBackdrop from "./FinalBackdrop.svelte";
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
  $: normoliActR = ($gui.R / 255).toFixed(2);
  $: normoliActG = ($gui.G / 255).toFixed(2);
  $: normoliActB = ($gui.B / 255).toFixed(2);
  $: normolizeBgR = ($guiBg.R / 255).toFixed(2);
  $: normolizeBgG = ($guiBg.G / 255).toFixed(2);
  $: normolizeBgB = ($guiBg.B / 255).toFixed(2);
  $: invertBgR = (1 - +normolizeBgR).toFixed(2);
  $: invertBgG = (1 - +normolizeBgG).toFixed(2);
  $: invertBgB = (1 - +normolizeBgB).toFixed(2);
  $: devinedR = (+invertBgR / +normoliActR).toFixed(2);
  $: devinedG = (+invertBgG / +normoliActG).toFixed(2);
  $: devinedB = (+invertBgB / +normoliActB).toFixed(2);
  $: finalInverR = (1 - +devinedR).toFixed(2);
  $: finalInverG = (1 - +devinedG).toFixed(2);
  $: finalInverB = (1 - +devinedB).toFixed(2);
  $: finalColorBgR = Math.round(+finalInverR * 255);
  $: finalColorBgG = Math.round(+-finalInverG * 255);
  $: finalColorBgB = Math.round(+finalInverB * 255);
</script>

<div class="wrapper">
  <BlandTitle tag="h3">Color Burn</BlandTitle>
  <BlandDescription
    >Inverting the background, dividing it by the foreground and inverting the
    result.</BlandDescription
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
          style="background-color: rgb({+finalInverR * 255}, 0, 0);"
        >
          <p class="inner__title">{finalInverR}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, {+-finalInverG * 255}, 0);"
        >
          <p class="inner__title">{-finalInverG}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, 0, {+finalInverB * 255});"
        >
          <p class="inner__title">{finalInverB}</p>
        </div>
      </div>
    </svelte:fragment>
  </BoxSeparetor>
  <BlandExemple {gui} {guiBg} blendmode="mix-blend-mode: color-burn;" />
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

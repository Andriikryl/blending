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
  $: invertActR = (1 - +normoliActR).toFixed(2);
  $: invertActG = (1 - +normoliActG).toFixed(2);
  $: invertActB = (1 - +normoliActB).toFixed(2);
  $: devinedR = (+normolizeBgR / +invertActR).toFixed(1);
  $: devinedG = (+normolizeBgG / +invertActG).toFixed(2);
  $: devinedB = (+normolizeBgB / +invertActB).toFixed(1);
  $: finalInverR = +devinedR * 255;
  $: finalInverG = +devinedG * 255;
  $: finalInverB = +devinedB * 255;
</script>

<div class="wrapper">
  <BlandTitle tag="h3">Color Dodge</BlandTitle>
  <BlandDescription
    >Invert the foreground divide the background by it.</BlandDescription
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
          style="background-color: rgb({+devinedR * 255}, 0, 0);"
        >
          <p class="inner__title">{devinedR}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, {+devinedG * 255}, 0);"
        >
          <p class="inner__title">{devinedG}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: rgb(0, 0, {+devinedB * 255});"
        >
          <p class="inner__title">{devinedB}</p>
        </div>
      </div>
    </svelte:fragment>
  </BoxSeparetor>
  <BlandExemple {gui} {guiBg} blendmode="mix-blend-mode: color-dodge;" />
  <FinalBackdrop bkB={finalInverB} bkG={finalInverG} bkR={finalInverR} />
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

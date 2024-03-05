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
  $: minR = Math.max($gui.R, $guiBg.R);
  $: minG = Math.max($gui.G, $guiBg.G);
  $: minB = Math.max($gui.B, $guiBg.B);
  $: algoritmsData = [
    "compares each colour",
    "selects the lightest value",
    `Blend ---> background-color: rgb(${$gui.R}, ${$gui.G}, ${$gui.B})`,
    `Background ---> background-color: rgb(${$guiBg.R}, ${$guiBg.G}, ${$guiBg.B})`,
    `Result ---> background-color: rgb(${minR}, ${minG}, ${minB})`,
  ];
</script>

<div class="wrapper">
  <BlandTitle tag="h3">LIGHTEN</BlandTitle>
  <SpeechBubble>B(Cb, Cs) = max(Cb, Cs)</SpeechBubble>
  <BlandDescription>Selects the lightest value.</BlandDescription>
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
        <div class="iiner__box" style="background-color: rgb({minR}, 0, 0);">
          <p class="inner__title">{minR}</p>
        </div>
        <div class="iiner__box" style="background-color: rgb(0, {minG}, 0);">
          <p class="inner__title">{minG}</p>
        </div>
        <div class="iiner__box" style="background-color: rgb(0, 0, {minB});">
          <p class="inner__title">{minB}</p>
        </div>
      </div></svelte:fragment
    >
  </BoxSeparetor>
  <BlandExemple {gui} {guiBg} blendmode="mix-blend-mode: lighten;" />
  <div class="backdrop__wrapper">
    <FinalBackdrop bkB={minB} bkG={minG} bkR={minR} />
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

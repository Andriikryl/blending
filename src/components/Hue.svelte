<script lang="ts">
  import BlandDescription from "./BlandDescription.svelte";
  import BlandExemple from "./BlandExemple.svelte";
  import BlandExempleHue from "./BlandExempleHue.svelte";
  import BlandTitle from "./BlandTitle.svelte";
  import BoxSeparetor from "./BoxSeparetor.svelte";
  import FinalBackdrop from "./FinalBackdrop.svelte";
  import SpeechBubble from "./SpeechBubble.svelte";
  import { GUI, guiControls } from "./index";
  const gui = guiControls({
    H: 350,
    S: 89,
    L: 60,
  });
  const guiBg = guiControls({
    H: 199,
    S: 89,
    L: 48,
  });

  $: algoritmsData = [
    "take the Blend hue",
    "take the background saturation and luminosity",
    `Blend ---> background-color: rgb(${$gui.H}, ${$gui.S}, ${$gui.L})`,
    `Background ---> background-color: rgb(${$guiBg.H}, ${$guiBg.S}, ${$guiBg.L})`,
    `Result ---> background-color: rgb(${$gui.H}, ${$guiBg.S}, ${$guiBg.L})`,
  ];
</script>

<div class="wrapper">
  <BlandTitle tag="h3">Hue</BlandTitle>
  <SpeechBubble>B(Cb, Cs) = SetLum(SetSat(Cs, Sat(Cb)), Lum(Cb))</SpeechBubble>
  <BlandDescription>
    Creates a color with the hue of the source color and the saturation and
    luminosity of the backdrop color.
  </BlandDescription>
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
          style="background-color: hsl({$gui.H}, 0%, 0%);"
        >
          <p class="inner__title">{$gui.H}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: hsl(0, {$guiBg.S}%, 0%);"
        >
          <p class="inner__title">{$guiBg.S}</p>
        </div>
        <div
          class="iiner__box"
          style="background-color: hsl(0, 0%, {$guiBg.L}%);"
        >
          <p class="inner__title">{$guiBg.L}</p>
        </div>
      </div></svelte:fragment
    >
  </BoxSeparetor>
  <BlandExempleHue {gui} {guiBg} blendmode=" mix-blend-mode: hue" />
  <div class="backdrop__wrapper">
    <FinalBackdrop
      bkB={$guiBg.L}
      bkG={$guiBg.S}
      bkR={$gui.H}
      ColorSpace="hsl"
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
    margin-block-end: 50px;
    background-color: hsl(199, 89, 48);
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

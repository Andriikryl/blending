<script lang="ts">
  import BlandDescription from "./BlandDescription.svelte";
  import BlandExemple from "./BlandExemple.svelte";
  import BlandTitle from "./BlandTitle.svelte";
  import BoxSeparetor from "./BoxSeparetor.svelte";
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
  $: minR = Math.min($gui.R, $guiBg.R);
  $: minG = Math.min($gui.G, $guiBg.G);
  $: minB = Math.min($gui.B, $guiBg.B);
</script>

<div>
  <BlandTitle tag="h3">darken</BlandTitle>
  <BlandDescription>
    Darken compares each colour's RGB value and selects the darkest value -
    creating a new colour.
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
      <BlandDescription>Backdrop</BlandDescription>
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
  <BlandExemple {gui} {guiBg} />
</div>

<style>
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

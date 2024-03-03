<script>
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
  <h3 class="main__title">darken</h3>
  <p class="description">
    Darken compares each colour's RGB value and selects the darkest value -
    creating a new colour.
  </p>
  <div class="controls__box">
    <div class="section__item section__item--start">
      <div class="control__bg">
        <GUI controls={gui} />
      </div>
      <div class="control__main">
        <GUI controls={guiBg} />
      </div>
    </div>
    <div class="section__item section__item--end">
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
      </div>
    </div>
  </div>
  <div class="wrapper">
    <div
      class="box"
      style="background-color: rgb({$guiBg.R}, {$guiBg.G}, {$guiBg.B});"
    ></div>
    <div
      class="boxBg"
      style="background-color: rgb({$gui.R}, {$gui.G}, {$gui.B});"
    ></div>
  </div>
</div>

<style>
  .main__title {
    color: var(--black, #1b1b1b);
    font-family: Patrick Hand;
    font-size: 30px;
    font-style: normal;
    font-weight: 400;
    line-height: normal;
    letter-spacing: -0.3px;
    margin-block-end: 20px;
    text-transform: uppercase;
    border-bottom: 1px solid #1b1b1b;
  }
  .description {
    color: var(--black, #1b1b1b);
    font-family: Patrick Hand;
    font-size: 18px;
    font-style: normal;
    font-weight: 400;
    line-height: 28px;
    border-left: 3px solid #ffc300;
    padding-inline-start: 10px;
  }
  .flex__group {
    display: flex;
    gap: 10px;
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
  .controls__box {
    display: flex;
    align-items: center;
    flex-direction: column;
    gap: 1rem;
    max-width: 700px;
    margin: 2rem auto;
  }
  .controls__box::before {
    content: "";
    border: 1px solid #d3d3d3;
    align-self: stretch;
  }
  @media (min-width: 1000px) {
    .controls__box {
      align-items: center;
      flex-direction: row;
    }
  }
  .section__item--start {
    order: -1;
  }
  .section__item {
    flex: 1;
  }
  .wrapper {
    display: flex;
    justify-content: center;
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
    mix-blend-mode: darken;
  }
  .inner__title {
    color: #fff;
  }
</style>

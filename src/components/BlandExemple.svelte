<script lang="ts">
  export let guiBg;
  export let gui;
  export let blendmode: string;
</script>

<div class="wrapper">
  <div
    class="box"
    style="background-color: rgb({$guiBg.R}, {$guiBg.G}, {$guiBg.B});"
  ></div>
  <div
    class="boxBg"
    style="background-color: rgb({$gui.R}, {$gui.G}, {$gui.B}); {blendmode};"
  ></div>
</div>

<style>
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
  }
</style>

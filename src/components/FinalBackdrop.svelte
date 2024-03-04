<script lang="ts">
  import BlandDescription from "./BlandDescription.svelte";
  export let bkR: number;
  export let bkG: number;
  export let bkB: number;
</script>

<div class="backdrop__box">
  <BlandDescription>Backdrop final color</BlandDescription>
  <div class="box" style="background-color: rgb({bkR}, {bkG}, {bkB});"></div>
</div>

<style>
  .backdrop__box {
    margin-block-start: 40px;
  }
  .box {
    width: 100px;
    height: 100px;
    margin-block-start: 10px;
  }
</style>

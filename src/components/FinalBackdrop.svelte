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
  .box {
    width: 100px;
    height: 100px;
    margin-block-start: 10px;
  }
</style>

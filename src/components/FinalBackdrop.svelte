<script lang="ts">
  import BlandDescription from "./BlandDescription.svelte";
  export let bkR: number;
  export let bkG: number;
  export let bkB: number;
  export let ColorSpace: string = "rgb";
</script>

<div class="backdrop__box">
  <BlandDescription>Backdrop final color</BlandDescription>
  {#if ColorSpace === "rgb"}
    <div class="box" style="background-color: rgb({bkR}, {bkG}, {bkB});"></div>
  {/if}
  {#if ColorSpace === "hsl"}
    <div
      class="box"
      style="background-color: hsl({bkR}, {bkG}%, {bkB}%);"
    ></div>
  {/if}
</div>

<style>
  .box {
    width: 100px;
    height: 100px;
    margin-block-start: 10px;
  }
</style>

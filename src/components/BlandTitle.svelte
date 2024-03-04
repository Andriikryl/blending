<script lang="ts">
  export let tag: string;
</script>

<svelte:element this={tag} class="main__title">
  <slot />
</svelte:element>

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
</style>

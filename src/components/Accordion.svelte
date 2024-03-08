<script lang="ts">
  import { setAccordionOptions } from "./store";
  export let collapse = false;
  setAccordionOptions({ collapse });
</script>

<div class="accordion">
  <slot />
</div>

<style>
  .accordion {
    display: flex;
    flex-direction: column;
    gap: 20px;
    width: var(--accordion-width, 100%);
    padding: var(--accordion-padding, 1rem);
    color: var(--accordion-color, hsl(220 10% 98%));
    background-color: transparent;
  }
</style>

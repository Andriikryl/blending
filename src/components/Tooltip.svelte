<script lang="ts">
  export let title = "";
  let isHovered = false;
  let x: number;
  let y: number;

  function mouseOver(event: MouseEvent) {
    isHovered = true;
    x = event.pageX + 5;
    y = event.pageY + 5;
  }
  function mouseMove(event: MouseEvent) {
    x = event.pageX + 5;
    y = event.pageY + 5;
  }
  function mouseLeave(event: MouseEvent) {
    isHovered = false;
  }
  function focus(event: FocusEvent) {
    isHovered = true;
  }
  function blur(event: FocusEvent) {
    isHovered = false;
  }
</script>

<div
  on:mouseover={mouseOver}
  on:mouseleave={mouseLeave}
  on:mousemove={mouseMove}
  on:focus={focus}
  on:blur={blur}
  tabindex="-1"
  role="tooltip"
>
  <slot />
</div>

{#if isHovered}
  <div style="top: {y}px; left: {x}px;" class="tooltip">{title}</div>
{/if}

<style>
  .tooltip {
    border: 1px solid #ddd;
    box-shadow:
      0 1px 1px rgba(0, 0, 0, 0.15),
      0 2px 2px rgba(0, 0, 0, 0.15),
      0 4px 4px rgba(0, 0, 0, 0.15),
      0 8px 8px rgba(0, 0, 0, 0.15);
    background: white;
    border-radius: 4px;
    color: var(--black, #1b1b1b);
    font-family: Patrick Hand;
    font-size: 20px;
    font-style: normal;
    font-weight: 400;
    line-height: normal;
    letter-spacing: -0.3px;
    margin-block-end: 20px;
    text-transform: uppercase;
    padding: 10px;
    position: absolute;
    z-index: calc(infinity);
  }
</style>

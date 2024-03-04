<script></script>

<div class="controls__box">
  <div class="section__item section__item--start">
    <slot name="item-start" />
  </div>
  <div class="section__item section__item--end">
    <slot name="item-end" />
  </div>
</div>

<style>
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
</style>

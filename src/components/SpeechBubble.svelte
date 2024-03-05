<script lang="ts"></script>

<div class="speech-bubble">
  <p>
    <slot />
  </p>
</div>

<style>
  .speech-bubble {
    padding: 10px;
    --speech-bubble-background: rgb(226 232 240);
    position: relative;
    background: var(--speech-bubble-background);
    border-radius: 9999px;
    height: 4rem;
    display: grid;
    place-items: center;
    max-width: 400px;
    margin-block-end: 20px;
    margin-inline-start: 20px;
  }
  .speech-bubble::before,
  .speech-bubble::after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;

    border-radius: 9999px;
    background: var(--speech-bubble-background);
  }
  .speech-bubble::before {
    height: 1.5rem;
    width: 1.5rem;
    transform: translate(-0.5rem, 0.5rem);
  }
  .speech-bubble::after {
    height: 0.75rem;
    width: 0.75rem;
    transform: translate(-1rem, 1rem);
  }
</style>

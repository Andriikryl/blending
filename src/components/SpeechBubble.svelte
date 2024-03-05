<script lang="ts"></script>

<div class="speech-bubble">
  <slot />
</div>

<style>
  .speech-bubble {
    position: relative;
  }
  .speech-bubble::before {
    content: "";

    position: absolute;
    bottom: 0;
    left: -1rem;

    border-width: 1rem;
    border-style: solid;
    border-color: transparent transparent rgb(226 232 240) transparent;
  }
</style>

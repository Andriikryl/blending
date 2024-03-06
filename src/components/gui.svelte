<script lang="ts">
  export let controls;
  const entries: any = Object.entries($controls);
  const isNotEmpty = entries.length > 0;

  const is = {
    number: (value: any) => typeof value === "number",
    boolean: (value: any) => typeof value === "boolean",
    text: (value: any) => typeof value === "string" && !value.startsWith("#"),
    color: (value: any) => typeof value === "string" && value.startsWith("#"),
    range: (value: any) => typeof value === "object",
  };

  function getBackgroundColor(label: string) {
    let color = "black";
    if (label === "R") {
      color = `rgb(244, 0, 0)`;
    } else if (label === "G") {
      color = "rgb(0, 63, 0)";
    } else if (label === "B") {
      color = "rgb(0, 0, 94)";
    }
    return `background-color: ${color}`;
  }

  function updateControls(e: Event) {
    let { value, type, dataset, checked, step, min, max } =
      e.target as HTMLInputElement;
    let key = dataset.key!;

    switch (type) {
      case "range":
        if (e.type === "wheel") {
          let direction = (e as WheelEvent).deltaY < 0 ? "up" : "down";

          if (direction === "up") {
            $controls[key].value < max && ($controls[key].value += +step);
          } else {
            $controls[key].value > min && ($controls[key].value -= +step);
          }
        } else {
          $controls[key].value = +value;
        }
        break;

      case "checkbox":
        $controls[key] = checked;
        break;

      case "number":
        $controls[key] = +value;
        break;

      default:
        $controls[key] = value;
    }
  }
</script>

{#if isNotEmpty}
  <div class="gui">
    {#each entries as [label, value]}
      {#if is.number(value)}
        <label style={getBackgroundColor(label)} class="lab__number">
          {label}
          <input
            on:change={updateControls}
            on:wheel={updateControls}
            value={$controls[label]}
            data-key={label}
            type="number"
          />
        </label>
      {/if}

      {#if is.boolean(value)}
        <label>
          {label}
          <input
            on:change={updateControls}
            data-key={label}
            checked={$controls[label]}
            type="checkbox"
          />
        </label>
      {/if}

      {#if is.text(value)}
        <label>
          {label}
          <input
            on:input={updateControls}
            data-key={label}
            value={$controls[label]}
            type="text"
          />
        </label>
      {/if}

      {#if is.range(value)}
        <label>
          {label}
          <input
            on:input={updateControls}
            on:wheel={updateControls}
            data-key={label}
            value={$controls[label].value}
            min={$controls[label].min}
            max={$controls[label].max}
            step={$controls[label].step}
            type="range"
          />
        </label>
      {/if}

      {#if is.color(value)}
        <label class="color__lab">
          {label}
          <input
            on:input={updateControls}
            value={$controls[label]}
            data-key={label}
            type="color"
          />
        </label>
      {/if}
    {/each}
  </div>
{/if}

<style>
  .gui {
    display: flex;
    flex-grow: 1;
    margin-block-end: 20px;
    gap: 10px;
    & .lab__number {
      max-width: 100px;
      flex-shrink: 0;
      flex-grow: 1;
      padding: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      gap: 5px;
      font-weight: 700;
      background-color: inherit;
      color: #fff;

      & input:not([type="checkbox"]) {
        width: 50px;
        height: 50px;
        text-align: center;
        cursor: pointer;
      }
    }
    & .color__lab {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 20px;
      font-weight: 700;
      color: var(--black, #1b1b1b);
      font-family: Patrick Hand;
      font-size: 20px;
      font-style: normal;
      font-weight: 400;
      line-height: normal;
      letter-spacing: -0.3px;
      margin-block-end: 20px;

      & input:not([type="checkbox"]) {
        width: 80px;
        height: 40px;
        text-align: center;
        cursor: pointer;
      }
    }
  }
</style>

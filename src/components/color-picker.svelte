<script>
  import NHScroller from "./h-scroller.svelte";
  import { base } from "./colors";

  export let value = "#20699d";
  export let grid = false;
  export let colors = base;
  export let className = "";

  $: selectedIndex = colors.indexOf(value) || 0;
</script>

<style lang="scss">
  :global(.n-color-picker) {
    overflow: scroll;
    max-width: 100%;
    width: 90vw;
    min-width: 100%;
    flex-grow: 1;
    flex-shrink: 1;
    display: flex;
    background-color: transparent;
    padding: 8px;
  }
  :global(.n-color-picker button.color-btn) {
    flex-grow: 0;
    flex-shrink: 0;
    border: solid 2px var(--color-solid);
    box-shadow: 0px 2px 6px rgba(0, 0, 0, 0.06);
    transition: all 0.2s ease-in-out;
    max-width: 20px;
    height: 20px;
    border-radius: 10px;
    &.selected {
      transform: scale(1.2);
      box-shadow: 0px 4px 16px rgba(0, 0, 0, 0.2);
      border: solid 1px var(--color-inverse);
    }
  }
</style>

{#if grid}
  <div class="n-grid n-color-picker {className}" activeIndex={selectedIndex}>
    {#each colors as color, index}
      <button
        class="color-btn {color == value ? 'selected' : ''}"
        style="background-color:{color}"
        on:click={() => {
          value = color;
        }} />
    {/each}
  </div>
{:else}
  <NHScroller className="n-color-picker {className}" activeIndex={selectedIndex}>
    {#each colors as color, index}
      <button
        class="color-btn {color == value ? 'selected' : ''}"
        on:click={() => {
          value = color;
        }}
        style="padding:0px; width:20px; background-color:{color}" />
    {/each}
  </NHScroller>
{/if}

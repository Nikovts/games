<script lang="ts">
  import { createEventDispatcher } from "svelte";

  // Create an event dispatcher to handle tab selection
  const dispatch = createEventDispatcher();

  export let tabs;
  export let row;
  export let selected;

  // Variable to store the currently selected tab
  let selectedTab;


  // Function to handle tab selection
  /**
   * @param {any} tab
   */
  function selectTab(tab, i) {
    selectedTab = tab;
    dispatch("tabSelected", { title: selectedTab.title, index: i });
  }

  $: {
    selectedTab = tabs[selected];
  }
</script>

<div class="tabs">
  <!-- Render the tab titles -->
  <ul class="tab-titles">
    {#each tabs as tab, i}
      <button
        class={row
          ? tab === selectedTab
            ? "base active"
            : "base"
          : tab === selectedTab
          ? "base-vertical active"
          : "base-vertical"}
        on:click={() => selectTab(tab, i)}
      >
        {#if tab.icon}
          <img src={tab.icon} alt={tab.title} class="logo" />
        {/if}
        <span class="label">{tab.title}</span>
      </button>
    {/each}
  </ul>
</div>

<style lang="scss">
  .tabs {
    margin-bottom: 10px;
    .tab-titles {
      display: flex;
      align-items: flex-start;
      width: 100%;
      background: #2b3b4b;
      border-radius: 12px;
      margin: 0;
      padding: 0;
      overflow: hidden;

      button {
        font-family: "Lato", sans-serif;
      }

      .base {
        display: flex;
        flex-direction: row;
        align-items: center;
        height: 3.5rem;
        padding: 18px;
        gap: 8px;
        cursor: pointer;
        color: #ffffff;
        background-color: inherit;
        border: none;
        border-right: 1px solid #465462;

        .label {
          font-style: normal;
          font-weight: 500;
          font-size: 14px;
          line-height: 20px;
        }
      }

      .base-vertical {
        display: flex;
        flex-direction: column;
        align-items: center;
        height: 5.5rem;
        padding: 16px 12px 12px;
        gap: 8px;
        cursor: pointer;
        color: #ffffff;
        background-color: inherit;
        border: none;
        border-right: 1px solid #465462;

        .logo {
          width: 34px;
          height: 34px;
          background: #1c2a37;
          box-shadow: 0px 0px 10px rgba(17, 177, 70, 0.5);
          border-radius: 8px;
        }

        .label {
          font-style: normal;
          font-weight: 400;
          font-size: 12px;
          line-height: 18px;
        }
      }
      .active {
        background: #0f853d;
      }
    }
  }
</style>

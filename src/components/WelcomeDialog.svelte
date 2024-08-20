<script lang="ts">
  import { createEventDispatcher } from "svelte";

  export let isOpen = false;
  export let title = "";
  export let message = "";

  const dispatch = createEventDispatcher();

  function closeDialog() {
    dispatch("close");
  }
</script>

{#if isOpen}
  <div class="dialog-overlay">
    <div class="dialog">
      <h2>{title}</h2>
      <p>{message}</p>
      <button on:click={closeDialog}>Close</button>
    </div>
  </div>
{/if}

<style>
  .dialog-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }

  .dialog {
    background-color: white;
    padding: 20px;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    display: flex;
    flex-direction: column;
    gap: 1em;
  }

  button {
    padding: 0.5em 1em;
    background-color: black;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
</style>

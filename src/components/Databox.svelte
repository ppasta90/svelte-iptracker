<script lang="ts">
  import DataItem from "./DataItem.svelte";
  export let ipData: any = {};
  console.log("ipData in Databox", ipData);
</script>

<section id="databox-section">
  {#if Object.entries(ipData).length === 0}
    <p>Enter an IP address to get started</p>
  {/if}
  {#each Object.entries(ipData) as [title, content]}
    <DataItem {title} {content} />
  {/each}
 
</section>

<style>
  #databox-section {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    padding: 1em;
    font-size: 1em;
    border: 1px solid #ccc;
    border-radius: 1rem;
  }
</style>

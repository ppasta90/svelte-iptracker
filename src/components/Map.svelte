<script lang="ts">
  import type { LngLatLike } from "svelte-maplibre";

  // @ts-ignore
  import { MapLibre } from "svelte-maplibre";
  export let coordinates: LngLatLike = [0,0]; //get user location if possible
</script>

<MapLibre
  center={coordinates}
  zoom={5}
  class="map"
  standardControls
  style="https://basemaps.cartocdn.com/gl/positron-gl-style/style.json"
/>

<style>
  :global(.map) {
    height: calc(100vh - 300px);
    width: 100%;
  }
</style>

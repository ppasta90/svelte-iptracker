<script lang="ts">
  import Input from "./components/Input.svelte";
  import Databox from "./components/Databox.svelte";
  import Map from "./components/Map.svelte";
  import type { IpData } from "./types/types";
  import type { LngLatLike } from "svelte-maplibre";

  import WelcomeDialog from "./components/WelcomeDialog.svelte";
  //@ts-ignore
  let ipData: IpData = {};
  let isOpen = localStorage.getItem("dialog") === "false" ? false : true;

  function handleIpData(event: CustomEvent<IpData>) {
    ipData = event.detail;
  }

  // derive a new state with only some properties of ipdata
  $: ipDataSubset = ipData.ip
    ? {
        city: ipData.location.city,
        country: ipData.location.country,
        region: ipData.location.region,
        coordinates: [ipData.location.lng, ipData.location.lat] as LngLatLike,
      }
    : {};
</script>

<main id="main">
  <WelcomeDialog
    {isOpen}
    message="Welcome to the Ip Tracker! Use the input field to search for an IP address."
    title="Svelte IP Tracker"
    on:close={() => {
      localStorage.setItem("dialog", "false");
      isOpen = false;
    }}
  />
  <h1>Svelte IP Tracker</h1>
  <Input on:ipDataUpdated={handleIpData} />
  <Databox ipData={ipDataSubset} />
  <Map coordinates={ipDataSubset.coordinates} />
</main>

<style>
  #main {
    display: flex;
    flex-direction: column;
    width: 100%;
    gap: 1em;
  }

  h1 {
    font-size: 2em;
    margin-bottom: 1em;
  }
</style>

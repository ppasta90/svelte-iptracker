<script lang="ts">
  import Input from "./components/Input.svelte";
  import Databox from "./components/Databox.svelte";
  import Map from "./components/Map.svelte";
  
  let ipData = {};

  function handleIpData(event) {
    ipData = event.detail;
  }

  // derive a new state with only some properties of ipdata
  $: ipDataSubset = ipData.ip ?  {
    ip: ipData.ip,
    isp: ipData.isp,
    location: ipData.location.country,
    region: ipData.location.region,
  } : {};
</script>

<main>
  <h1>Svelte IP Tracker</h1>
  <Input on:ipDataUpdated={handleIpData} />
  <Databox ipData={ipDataSubset} />
  <Map />
</main>

<style>
</style>
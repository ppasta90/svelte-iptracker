<script lang="ts">
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  let inputValue = "";

  const handleInput = (event) => {
    inputValue = event.target.value;
  };

  const handleKeydown = (event) => {
    if (event.key === "Enter") {
      fetchIpData();
    }
  };

  const fetchIpData = async () => {
    const response = await fetch(
      `https://geo.ipify.org/api/v1?apiKey=${import.meta.env.VITE_GEOIPIFY_API_KEY}&ipAddress=${inputValue}`
    );
    const data = await response.json();
    dispatch("ipDataUpdated", data);
  };
</script>

<section id="input-section">
  <form on:submit|preventDefault={fetchIpData}>
    <input
      type="text"
      placeholder="Search for any IP address or domain"
      on:change={handleInput}
      on:keydown={handleKeydown}
    />
  </form>
  <button type="submit"> Search </button>
</section>

<style>
  #input-section {
    display: flex;
    justify-content: center;
    margin-bottom: 2rem;
  }
  form {
    display: flex;
    justify-content: center;
    align-items: center;

    width: 100%;
  }
  input {
    max-width: 1440px;
    width: 100%;
    padding: 1em;
    font-size: 1em;
    border: 1px solid #ccc;
    border-radius: 1rem;
  }
  button {
    font-size: 1em;
    border: none;
    border-radius: 1rem;
    background-color: #000;
    color: #fff;
    cursor: pointer;
    margin-left: 1em;
  }
</style>

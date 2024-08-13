<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import type { IpData } from "../types/types";
  const dispatch = createEventDispatcher<{
    ipDataUpdated: IpData;
  }>();

  let inputValue = "";

  const handleInput = (event: Event): void => {
    const target = event.target as HTMLInputElement;
    inputValue = target.value;
  };

  const handleKeydown = (event: KeyboardEvent): void => {
    if (event.key === "Enter") {
      fetchIpData();
    }
  };

  const fetchIpData = async (): Promise<void> => {
    try {
      const response = await fetch(
        `https://geo.ipify.org/api/v1?apiKey=${import.meta.env.VITE_GEOIPIFY_API_KEY}&ipAddress=${inputValue}`
      );
      const data = await response.json();
      dispatch("ipDataUpdated", data);
    } catch (error) {
      console.error("Error fetching IP data:", error);
    }
  };
</script>

<section id="input-section">
  <form on:submit|preventDefault={fetchIpData}>
    <input
      type="text"
      placeholder="Search for any IP address or domain"
      on:input={handleInput}
      on:keydown={handleKeydown}
      value={inputValue}
    />
    <button type="submit">Search</button>
  </form>
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
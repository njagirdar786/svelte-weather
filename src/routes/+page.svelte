<script context="module">
  export const ssr = false;
</script>

<script>
  import { onMount } from "svelte";
  import Search from "../lib/components/Search.svelte";
  import CurrentWeather from "../lib/components/CurrentWeather.svelte";
  import WeatherDetails from "../lib/components/WeatherDetails.svelte";
  import WeatherForecast from "../lib/components/WeatherForecast.svelte";

  let location = "Leeds";
  let weather = null;

  async function fetchWeather(location) {
    const apiKey = import.meta.env.VITE_NEXT_PUBLIC_WEATHER_API_KEY;
    const url = `http://api.weatherapi.com/v1/forecast.json?key=${apiKey}&q=${location}&days=3&aqi=no&alerts=no`;
    const response = await fetch(url);
    weather = await response.json();
  }

  onMount(() => {
    fetchWeather(location);
  });

  function getLocation(newLocation) {
    location = newLocation;
    fetchWeather(location);
  }
</script>

<div class="flex flex-col bg-black items-center p-4 text-white min-h-screen">
  <Search {getLocation} />

  {#if weather}
    <div class=" grid sm:grid-cols-1 md:grid-cols-2 lg:grid-cols-2 gap-4">
      <CurrentWeather data={weather} />
      <WeatherDetails data={weather} />
      <WeatherForecast data={weather} />
    </div>
  {:else}
    <p>Loading...</p>
  {/if}
</div>

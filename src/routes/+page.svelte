<script>
  import { onMount } from "svelte";

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
</script>

<div class="flex flex-col bg-black items-center p-4 text-white min-h-screen">
  <h1>{weather ? weather.location.region : "Loading"}</h1>
</div>

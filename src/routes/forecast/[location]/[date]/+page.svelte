<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";

  let dayData = null;
  let location;
  let date;

  location = $page.params.location;
  date = $page.params.date;

  onMount(() => {
    fetchWeatherData(location, date);
  });

  async function fetchWeatherData(location, date) {
    const apiKey = import.meta.env.VITE_NEXT_PUBLIC_WEATHER_API_KEY;
    const url = `http://api.weatherapi.com/v1/forecast.json?key=${apiKey}&q=${location}&days=3&aqi=no&alerts=no`;
    const response = await fetch(url);
    const data = await response.json();
    dayData = data.forecast.forecastday.find((day) => day.date === date);
  }
</script>

{#if dayData}
  <div class="card bg-gradient-to-br from-purple-500 to-gray-900">
    <div class="card-body">
      <h2 class="card-title">Forecast for {dayData.date} in {location}</h2>

      <a href="/" class="btn">Go Home</a>
    </div>
  </div>
{:else}
  <p>Loading...</p>
{/if}

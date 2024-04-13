<script>
  import ForecastCard from "./ForecastCard.svelte";
  export let data;
</script>

<div
  class="card bg-gradient-to-br from-green-300 to-gray-900 lg:col-span-2 md:col-span-2"
>
  <div class="card-body">
    <h2 class="card-title">3 Days Forecast</h2>
    <div class="flex justify-around">
      {#each data.forecast.forecastday as day}
        <ForecastCard {day} location={data.location.name} />
      {/each}
    </div>
  </div>
</div>

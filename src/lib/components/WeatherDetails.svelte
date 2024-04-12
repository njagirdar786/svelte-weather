<script>
  export let data;
</script>

<div class="card bg-gradient-to-br from-cyan-300 to-gray-900">
  <div class="card-body">
    <h2 class="card-title">Weather Details</h2>
    <div class="stats stats-vertical lg:stats-horizontal shadow">
      <div class="stat">
        <div class="stat-title">Humidity</div>
        <div class="stat-value">{data.current.humidity}%</div>
      </div>

      <div class="stat">
        <div class="stat-title">Wind Speed</div>
        <div class="stat-value">{data.current.wind_mph} mph</div>
      </div>

      <div class="stat">
        <div class="stat-title">Wind Direction</div>
        <div class="stat-value">{data.current.wind_dir}</div>
      </div>
    </div>
    <div class="stats stats-vertical lg:stats-horizontal shadow">
      <div class="stat">
        <div class="stat-title">Sunrise</div>
        <div class="stat-value">
          {data.forecast.forecastday[0].astro.sunrise}
        </div>
      </div>

      <div class="stat">
        <div class="stat-title">Sunset</div>
        <div class="stat-value">
          {data.forecast.forecastday[0].astro.sunset}
        </div>
      </div>

      <div class="stat">
        <div class="stat-title">Feels Like</div>
        <div class="stat-value">{data.current.feelslike_c}°C</div>
      </div>

      <div class="stat">
        <div class="stat-title">Visibility</div>
        <div class="stat-value">{data.current?.vis_miles} mi</div>
      </div>
    </div>
  </div>
</div>

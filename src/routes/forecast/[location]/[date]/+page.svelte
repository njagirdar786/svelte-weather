<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  import { Chart } from "frappe-charts";

  let dayData = null;
  let location = $page.params.location;
  let date = $page.params.date;

  onMount(async () => {
    await fetchWeatherData(location, date);
    if (dayData) {
      initializeChart();
    }
  });

  async function fetchWeatherData(location, date) {
    const apiKey = import.meta.env.VITE_PUBLIC_WEATHER_API_KEY;
    const url = `http://api.weatherapi.com/v1/forecast.json?key=${apiKey}&q=${location}&days=3&aqi=no&alerts=no`;
    const response = await fetch(url);
    const data = await response.json();
    dayData = data.forecast.forecastday.find((day) => day.date === date);
  }

  function initializeChart() {
    const hourlyData = dayData.hour;
    const chartData = {
      labels: hourlyData.map((hour) => hour.time),
      datasets: [
        {
          name: "°C",
          type: "line",
          values: hourlyData.map((hour) => hour.temp_c),
        },
      ],
    };

    new Chart("#hourly-temperature-chart", {
      title: "Hourly Temperature in °C",
      data: chartData,
      type: "line",
      height: 250,
      axisOptions: {
        xIsSeries: true,
        xAxisMode: "tick",
        yAxisMode: "tick",
      },
      lineOptions: {
        hideDots: 0,
        heatline: 0,
        regionFill: 1,
      },
      colors: ["#69ff47"],
    });
  }
</script>

{#if dayData}
  <div class="card bg-gradient-to-br text-white from-purple-500 to-gray-900">
    <div class="card-body">
      <h2 class="card-title">
        Forecast for {dayData.date} in {location}
      </h2>
      <div class="kbd bg-gradient-to-br from-green-300 to-gray-900 mt-2">
        <img
          src={`https:${dayData.day.condition.icon}`}
          alt="icon"
          height="40"
          width="40"
        />
        {dayData.day.condition.text}
      </div>
      <div class="stats shadow">
        <div class="stat">
          <div class="stat-title">Maximum Temperature</div>
          <div class="stat-value">{dayData.day.maxtemp_c}°C</div>
        </div>
        <div class="stat">
          <div class="stat-title">Minimum Temperature</div>
          <div class="stat-value">{dayData.day.mintemp_c}°C</div>
        </div>
        <div class="stat">
          <div class="stat-title">Average Temperature</div>
          <div class="stat-value">{dayData.day.avgtemp_c}°C</div>
        </div>
      </div>

      <div class="stats shadow">
        <div class="stat">
          <div class="stat-title">Max Wind Speed</div>
          <div class="stat-value">{dayData.day.maxwind_mph} mph</div>
        </div>
        <div class="stat">
          <div class="stat-title">Total Precipitation:</div>
          <div class="stat-value">{dayData.day.totalprecip_mm} mm</div>
        </div>
        <div class="stat">
          <div class="stat-title">Average Visibility</div>
          <div class="stat-value">{dayData.day.avgvis_miles} mi</div>
        </div>
      </div>

      <div class="stats shadow">
        <div class="stat">
          <div class="stat-title">Average Humidity</div>
          <div class="stat-value">{dayData.day.avghumidity}%</div>
        </div>
        <div class="stat">
          <div class="stat-title">UV Index</div>
          <div class="stat-value">{dayData.day.uv}</div>
        </div>
        <div class="stat">
          <div class="stat-title">Chance of Rain</div>
          <div class="stat-value">{dayData.day.daily_chance_of_rain} %</div>
        </div>
      </div>

      <div class="stats shadow">
        <div class="stat">
          <div class="stat-title">Sunrise</div>
          <div class="stat-value">{dayData.astro.sunrise}</div>
        </div>
        <div class="stat">
          <div class="stat-title">Sunset</div>
          <div class="stat-value">{dayData.astro.sunset}</div>
        </div>
        <div class="stat">
          <div class="stat-title">Moonrise</div>
          <div class="stat-value">{dayData.astro.moonrise}</div>
        </div>
        <div class="stat">
          <div class="stat-title">Moonset</div>
          <div class="stat-value">{dayData.astro.moonset}</div>
        </div>
        <div class="stat">
          <div class="stat-title">Moon Phase</div>
          <div class="stat-value">{dayData.astro.moon_phase}</div>
        </div>
      </div>

      <div class="stats">
        <div class="stat">
          <div id="hourly-temperature-chart"></div>
        </div>
      </div>

      <a href="/" class="btn">Go Home</a>
    </div>
  </div>
{/if}

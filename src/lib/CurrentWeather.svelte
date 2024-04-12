<script>
  export let data;
</script>

<div class="card bg-gradient-to-br from-purple-500 to-gray-900">
  <div class="card-body items-center text-center">
    <h2 class="card-title">Today</h2>
    <div class="stats shadow">
      <div class="card-body">
        <h2 class="card-title">
          {data.location.name}, {data.location.region}
        </h2>
        <h2 class="stat-title">{data.location.tz_id}</h2>
        <p class="stat-value">{data.current.temp_c}°C</p>
        <div class="kbd bg-gradient-to-br from-pink-500 to-gray-900">
          <img
            src={"https:" + data.current.condition.icon}
            alt="icon"
            height="40"
            width="40"
            class="mt-1"
          />
          <p class="pl-2 pr-2">{data.current.condition.text}</p>
        </div>
        <p>{data.location.localtime}</p>
      </div>
    </div>
  </div>
</div>

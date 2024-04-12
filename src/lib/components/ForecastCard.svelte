<script>
  export let day;
  export let location;
</script>

<div class="stats">
  <div class="stat">
    <div class="card-title">{day.date}</div>
    <div class="stat-value">{day.day.condition.text}</div>
    <div class="kbd bg-gradient-to-br from-blue-500 to-gray-900 mt-2">
      <img
        src={"https:" + day.day.condition.icon}
        alt="icon"
        height="40"
        width="40"
      />
    </div>
    <a href={"/"} class="btn">View More</a>
  </div>
</div>

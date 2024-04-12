<script>
  export let getLocation;

  let query = "";

  function handleSubmit(e) {
    e.preventDefault();
    getLocation(query);
  }
</script>

<form on:submit={handleSubmit}>
  <div class="flex">
    <input
      bind:value={query}
      placeholder="Enter a location..."
      class="input w-full max-w-xs mb-8 mt-4"
    />
    <button class="btn mb-8 mt-4 ml-4" type="submit">Search</button>
  </div>
</form>

<script>
  import Search from "../lib/components/Search.svelte";

  let location = "Leeds";
  let weather = null;
</script>

<div class="flex flex-col bg-black items-center p-4 text-white min-h-screen">
  <Search />
</div>

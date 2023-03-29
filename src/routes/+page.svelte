<script>
    // Import Bootstrap
    import "bootstrap/dist/css/bootstrap.min.css";
    // Import Data
    import Deezer from "../data/Deezer.svelte";

    let artistSearch;
</script>

<div class="container w-75 my-3">
    <h3 class="mb-3">Search for your favourite albums</h3>
    <!-- {#if artistSearch} -->
    <Deezer {artistSearch} />
    <!-- {/if} -->
</div>

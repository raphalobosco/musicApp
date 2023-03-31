<script>
    export let artistSearch;
    export let click;
</script>

<div class="d-flex gap-3 mb-3">
    <input
        class="form-control"
        placeholder="Search for artist name"
        bind:value={artistSearch}
        on:input
    />
    <button class="btn btn-primary" on:click={click}>Search</button>
</div>

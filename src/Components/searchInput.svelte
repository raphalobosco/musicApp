<script>
    export let searchTerm;
</script>

<div class="d-flex gap-3">
    <input
        class="form-control"
        placeholder="Artist, albums, singles..."
        bind:value={searchTerm}
        on:input
    />
</div>

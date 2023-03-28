<script>
    export let album;
    export let name;
</script>

<div class="d-flex align-items-center p-3 border rounded-3 shadow-sm mb-3">
    <img class="rounded me-3" src="https://picsum.photos/90" alt="" />
    <div class="flex-fill">
        <h4>{album}</h4>
        <p>{name}</p>
    </div>
    <button class="btn btn-sm btn-outline-success align-self-start">
        save
    </button>
</div>

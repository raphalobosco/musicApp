<script>
    export let item;
</script>

<div class="d-flex align-items-center p-3 border rounded-3 shadow-sm mb-3">
    <img
        class="rounded img-fluid me-3"
        src={item.album.cover_medium}
        alt=""
        style="max-width:90px"
    />
    <div class="flex-fill">
        <h4>{item.album.title}</h4>
        <p>{item.artist.name}</p>
    </div>
    <button class="btn btn-sm btn-outline-success align-self-start">
        save
    </button>
</div>

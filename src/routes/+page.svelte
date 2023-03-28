<script>
    // Import Bootstrap
    import "bootstrap/dist/css/bootstrap.min.css";

    // Import components
    import Results from "../Components/Results.svelte";
    import SearchInput from "../Components/searchInput.svelte";
    import { spotifyList } from "../data/spotify.js";

    // Logic
    let albumData = spotifyList;

    let albumResults = [];

    let searchTerm = "";

    const searchAlbums = () => {
        return (albumResults = albumData.filter((results) => {
            let albumTitle = results.album;
            let albumArtist = results.name;
            return (
                albumTitle.includes(searchTerm) ||
                albumArtist.includes(searchTerm)
            );
        }));
    };

    // console.log(searchAlbums());
</script>

<div class="container w-50 my-3">
    <h3 class="mb-3">Search for your favourite albums</h3>
    <!-- input -->
    <SearchInput bind:searchTerm on:input={searchAlbums} />
    <hr />
    <div>
        {#if searchTerm && albumResults.length === 0}
            <p>Nothing here</p>
        {:else if albumResults.length > 0}
            {#each albumResults as { album, name }}
                <Results {album} {name} />
            {/each}
        {:else}
            {#each albumData as { album, name }}
                <Results {album} {name} />
            {/each}
        {/if}
    </div>
</div>

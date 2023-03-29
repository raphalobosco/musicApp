<script>
    import Results from "../Components/Results.svelte";
    import SearchInput from "../Components/searchInput.svelte";

    export let artistSearch = "";

    let artistData = [];

    async function getArtist({ query }) {
        query = artistSearch;
        const response = await fetch(
            `https://api.deezer.com/search?q=${query}`
        );
        const data = await response.json();
        artistData = data.data;
        console.log(artistData);
    }

    // getArtist();

    function handleSearch() {
        getArtist({ artistSearch });
    }

    // console.log(artistSearch);
</script>

<SearchInput bind:artistSearch on:input={handleSearch} />
<!-- <SearchInput bind:artistSearch click={handleSearch} /> -->

{#each artistData as item}
    <Results {item} />
{/each}

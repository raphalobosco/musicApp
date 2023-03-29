<script>
    import Results from "../Components/Results.svelte";
    import SearchInput from "../Components/searchInput.svelte";

    export let artistSearch = "";
    let artistData = [];

    async function getArtist({ query }) {
        const options = {
	method: 'GET',
	headers: {
		'X-RapidAPI-Key': '2ada17cf2emsh3bad8b4a0f82850p1e5bbdjsnb70430199869',
		'X-RapidAPI-Host': 'deezerdevs-deezer.p.rapidapi.com'
	}
};
        query = artistSearch;
        const response = await fetch(
            `https://deezerdevs-deezer.p.rapidapi.com/search?q=${query}`, options
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

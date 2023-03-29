<script>
    import Results from "../Components/Results.svelte";
    import SearchInput from "../Components/searchInput.svelte";
   

    export let artistSearch;
    let artistData = [];
    let suggestion = []
    
    let clicked = false
    let modal = false
    
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
    
    }

    // getArtist();

    function handleSearch() {
        modal = false
        clicked = true
        getArtist({ artistSearch });
    }
    
    function handleSuggestion() {
    modal = true;
    if (artistSearch) {
        getArtist({ artistSearch });
        
        const uniqueSuggestions = new Set();
        artistData.forEach((album) => {
            uniqueSuggestions.add(album.artist.name);
            // uniqueSuggestions.add(album.title);
        });
        suggestion = Array.from(uniqueSuggestions);
    } else {
        suggestion = [];
        modal = false;
    }
}

    

    // console.log(artistSearch);
</script>

<!-- <SearchInput bind:artistSearch on:input={handleSearch} /> -->
<SearchInput bind:artistSearch on:input={handleSuggestion} click={handleSearch} />


{#if modal}
    <div class="position-absolute p-3 bg-white shadow">
        {#each suggestion as item}
            <p class="suggestion-item " on:click={handleSearch}>{item}</p>
        {/each}
    </div>
{/if}

{#if clicked}
{#each artistData as item}
    <Results {item} />
{/each}
{/if}

<style lang="scss">
.suggestion-item {
    cursor: pointer;
    display: block;
    font-weight: 400;
    color: #666;
    text-decoration: none;
    padding: 3px 6px;
    border-radius: 6px;
}

.suggestion-item:hover {
    background-color: #eee;
    color: #000;
    }
</style>
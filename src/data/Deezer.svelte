<script>
    import Results from "../Components/Results.svelte";
    import SearchInput from "../Components/searchInput.svelte";

    export let artistSearch;
    let artistData = [];
    let suggestion = [];
    let clicked = false;
    let modal = false;

    async function getArtist({ query }) {
        const API_CODE = import.meta.env.VITE_RAPID_KEY;
        const options = {
            method: "GET",
            headers: {
                "X-RapidAPI-Key": API_CODE,
                "X-RapidAPI-Host": "deezerdevs-deezer.p.rapidapi.com",
            },
        };
        query = artistSearch;
        const response = await fetch(
            `https://deezerdevs-deezer.p.rapidapi.com/search?q=${query}`,
            options
        );
        const data = await response.json();
        artistData = data.data;
    }

    function handleSearch() {
        artistData = [];
        clicked = true;
        if (artistSearch) {
            modal = false;
            getArtist({ artistSearch });
            artistSearch = "";
        } else {
            artistData = [];
            clicked = false;
        }
    }

    function handleClick(e) {
        artistSearch = e;
        handleSearch();
    }

    function handleSuggestion() {
        modal = true;
        clicked = false;
        if (artistSearch) {
            getArtist({ artistSearch });
            const uniqueSuggestions = new Set();
            artistData.forEach((album) => {
                uniqueSuggestions.add(album.artist.name);
            });
            suggestion = Array.from(uniqueSuggestions);
        } else {
            suggestion = [];
            modal = false;
        }
    }
</script>

<!-- <SearchInput bind:artistSearch on:input={handleSearch} /> -->
<SearchInput
    bind:artistSearch
    on:input={handleSuggestion}
    click={handleSearch}
/>

{#if modal}
    <div class="position-absolute p-3 bg-white shadow">
        {#each suggestion as item, i (i)}
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <p
                key={i}
                class="suggestion-item "
                on:click={() => handleClick(item)}
            >
                {item}
            </p>
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

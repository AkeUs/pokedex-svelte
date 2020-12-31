<script>
    import PokedexSearch from "./PokedexSearch.svelte";
    import PokedexCard from "./PokedexCard.svelte";
    import { onMount } from "svelte";

    let error = false;
    let loading = false;
    let pokemon = null;
    const randomId = Math.floor(Math.random() * 151);
    let pokemonId = randomId;

    const getPokemonById = async () => {
        let url = `https://pokeapi.co/api/v2/pokemon/${pokemonId}`;
        await fetch(url)
            .then(response => response.json())
            .then(data => {
                pokemon = data;
                loading = false;
                error = false;
            })
            .catch(err => {
                console.error(err);
                loading = false;
                error = true;
            });
    }

    onMount(() => {
        getPokemonById();
    });

    $: if (pokemonId) {
        getPokemonById();
    }
</script>

<style>
    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .pokedex-title {
        font-size: 4.5em;
        color: #F7C406;
        -webkit-text-stroke: 3px #3C5AAF;
    }
</style>

<div class="container">
    <h1 class="pokedex-title">Poked&eacute;x</h1>
    <PokedexSearch
        bind:pokemonId={pokemonId}
        bind:loading={loading}
        bind:error={error}/>
    <PokedexCard
        pokemon={pokemon}
        loading={loading}
        error={error} />
</div>

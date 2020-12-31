<script>
    import PokedexStat from "./PokedexStat.svelte";

    export let pokemon;
    export let loading;
    export let error;
</script>

<style>
    .pokedex-card {
        background-color: #FFFFFF;
        max-width: 600px;
        padding:10px;
        border-radius: 5px;
        box-shadow: 0 5px 10px 0 rgba(0, 0, 0, 0.5);
        transition: 0.3s;
    }
    .pokedex-card:hover {
        box-shadow: 0 10px 18px 0 rgba(0, 0, 0, 0.5);
    }
    .pokedex-card-header {
        text-align: center;
    }
    .pokedex-card-info {
        display: flex;
        flex-direction: row;
    }
    .pokemon-stats {
        list-style: none;
    }
    .text-help {
        color: #FFFFFF;
        font-size: 24px;
    }
    .pokemon-type {
        background-color: #cfd8dc;
        border-radius: 5px;
        padding: 2px 30px 2px 30px;
        margin: 5px;
    }
</style>

{ #if error }
    <h2 class="text-help">Error</h2>
{ :else if !pokemon || loading}
    <h2 class="text-help">Espere...</h2>
{ :else }
    <div class="pokedex-card">
        <div class="pokedex-card-header">
            <h2>{ pokemon.name.toUpperCase() }</h2>
            <h3>
                { #each pokemon.types as type (type.slot) }
                    <span class="pokemon-type">{ type.type.name }</span>
                { /each }
            </h3>
        </div>
        <div class="pokedex-card-info">
            <img src={ pokemon.sprites.front_default } alt={ pokemon.name }>
            <ul class="pokemon-stats">
                { #each pokemon.stats as item (item.stat.name) }
                    <PokedexStat item={item} />
                { /each }
            </ul>
        </div>
    </div>
{ /if }

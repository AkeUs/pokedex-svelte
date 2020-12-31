<script>
    let pokemonName = '';
    export let pokemonId;
    export let loading;
    export let error;

    const searchPokemon = (e) => {
        e.preventDefault();

        if (pokemonName !== '') {
            error = false;
            loading = true;
            pokemonId = window.isNaN(parseInt(pokemonName))
                ? pokemonName.toLowerCase() :
                pokemonName;
            pokemonName = '';
            return;
        }

        error = true;
    }
</script>

<style>
    .search-form {
        margin: 0 0 30px 0;
        box-shadow: 0 5px 10px 0 rgba(0, 0, 0, 0.5);
        transition: 0.3s;
    }
    .search-form:hover {
        box-shadow: 0 10px 18px 0 rgba(0, 0, 0, 0.5);
    }
    .search-form > input[type="text"] {
        padding: 10px;
        border-radius: 5px 0 0 5px;
        border: none;
    }
    .search-form > input[type="submit"] {
        padding: 10px;
        border-radius: 0 5px 5px 0;
        border: none;
    }
</style>

<form class="search-form"
    on:submit={searchPokemon} >

    <input
        type="text"
        name="pokemon"
        placeholder="Pokemon ID or name"
        autocomplete="off"
        bind:value={pokemonName} />

    <input type="submit" value="search">
</form>

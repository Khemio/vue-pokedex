<template>
    <div class="w-full flex justify-center">
    <input v-model="text"
        type="text"
        placeholder="Enter Pokemon Here"
        class="mt-10 p-2 border-blue-500 border-2 text-yellow-600">
    </div>
    <div class="mt-10 p-4 flex flex-wrap justify-center"  v-if="filteredPokemons">
            <div class="ml-4 text-2xl text-blue-500"
            v-for="(pokemon, idx) in filteredPokemons" 
            :key="idx">
            <RouterLink :to="{name: 'About', params: {slug: urlIdLookup[pokemon.name]}}">
                {{pokemon.name}}
            </RouterLink>
            
            
        </div>
    </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import { RouterLink } from 'vue-router';

const pokemons= ref(null);
const urlIdLookup = ref({});
const text = ref('');
const filteredPokemons = computed(() => updatePokemon())

const fetchPokemon = async () => {
  const res = await fetch("https://pokeapi.co/api/v2/pokemon?offset=0");
  const data = await res.json();
  pokemons.value = data.results;
  urlIdLookup.value = data.results.reduce((acc, cur, idx) => acc = {...acc, [cur.name]:idx+1}, {})
};

const updatePokemon = () => {
    if(!text.value) {
        return [];
    }

    return pokemons.value.filter(pokemon => pokemon.name.includes(text.value));

}

fetchPokemon();

</script>
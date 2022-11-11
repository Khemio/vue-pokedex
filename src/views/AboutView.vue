<template>
    <div class="about">
        <div v-if="pokemon"
        class="w-3/12 m-auto bg-gray-600 mt-3 py-2 shadow-2xl shadow-gray-600 flex flex-col justify-center items-center rounded-xl">
            <h3 class="text-2xl text-green-900 uppercase">{{pokemon.name}}</h3>
            <div class="flex jstify-center">
                <img class="w-48" :src="pokemon.sprites.front_shiny" alt="">
                <img class="w-48" :src="pokemon.sprites.back_shiny" alt="">
            </div>
            <h3 class="text-yellow-400">Types</h3>
            <div v-for="(type,idx) in pokemon.types" :key="idx">
                <h5 class="text-blue-900">{{type.type.name}}</h5>
            </div>
        </div>
    </div>
</template>

<script setup>
import { useRoute } from 'vue-router';
import { ref } from 'vue';

const route = useRoute();
const pokemon = ref(null);

const fetchPokemon = async () => {
  const res = await fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`);
  const data = await res.json();
  pokemon.value = data;
};

fetchPokemon();

</script>
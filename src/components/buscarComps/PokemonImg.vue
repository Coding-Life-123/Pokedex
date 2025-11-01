<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
    data: Object,
    colors: Array
})

const pokemon = ref(props.data.data);
const colors = ref(props.colors)
console.log(props)

watch(() => props.data,(newVal)=>{pokemon.value = newVal.data})
console.log(pokemon)

const imgSrc = ref(pokemon.value.sprites.other.home.front_default);
const pokemonName = ref(pokemon.value.name.slice(0, 1).toUpperCase() + pokemon.value.name.slice(1,pokemon.value.name.length))
console.log(pokemonName.value)

console.log(colors.value);




console.log(props.data.data.sprites.other.home.front_default)
</script>

<template>
    <div v-if="data" class="pokemon-image" :style="{
        background: `linear-gradient(135deg, ${colors[0]}, ${colors[1]})`,
        boxShadow: `0 0 40px ${colors[0]}`
        }
    " style="
        padding: 20px;
        border-radius: 20px;
    ">
        <h1 style="text-align: center;">{{ pokemonName }}</h1>
        <img :src="imgSrc" alt="" />
        <div style="display: flex; justify-content: space-between; width: 100%;">
            <p style="font-size: larger;">{{ pokemon.height }}m</p>
            <p style="font-size: larger;">{{ pokemon.weight }}kg</p>
        </div>
    </div>
</template>

<style>
    .pokemon-image h2{
    }
</style>
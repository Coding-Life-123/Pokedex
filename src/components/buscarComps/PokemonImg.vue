<script setup>
import { computed, watch } from 'vue';

let props = defineProps({
    data: Object,
    colors: Array
})

const pokemon = computed(()=>props.data.data);
const colors = computed(()=>props.colors);

watch([()=> props.data, ()=> props.colors],([newData, newColors])=>{
    pokemon: newData;
    colors: newColors;
    
})

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
        <h1 style="text-align: center;">{{ pokemon.name.charAt(0).toUpperCase()+pokemon.name.slice(1) }}</h1>
        <img :src="pokemon.sprites.other.home.front_default" alt="" />
        <div style="display: flex; justify-content: space-between; width: 100%;">
            <p style="font-size: larger;">{{ pokemon.height }}m</p>
            <p style="font-size: larger;">{{ pokemon.weight }}kg</p>
        </div>
    </div>
</template>

<style>
</style>
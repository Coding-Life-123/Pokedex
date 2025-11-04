<script setup>
import { computed, watch } from 'vue';

let props = defineProps({
    data: Object,
    colors: Array
})

console.log(props.data)
const pokemon = computed(()=>props.data);
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
    ">
        <h1 style="text-align: center;">{{ pokemon.name.charAt(0).toUpperCase()+pokemon.name.slice(1) }}</h1>
        <img :src="pokemon.sprites.other.home.front_default" alt="" />
        <div>
            <p style="font-size: larger;">{{ pokemon.height }}m</p>
            <p style="font-size: larger;">{{ pokemon.weight }}kg</p>
        </div>
    </div>
</template>

<style>
    .pokemon-image {
        height: fit-content;
        width: fit-content;
        padding: 20px;
        border-radius: 20px;
        display: flex;
        flex-direction: column;
    }

    .pokemon-image img {
        margin: auto;
        width: 100%;
    }

    .pokemon-image div{
        display: flex; 
        justify-content: space-between; 
        margin-bottom: 0; 
        width: 100%;
    }

    @media (max-width:500px) and (min-width:300px){
        .pokemon-image{
           
        }
    
        .pokemon-image h1{
            width: 240px;
        }

        .pokemon-image img{
            width: 240px;
        }

        .pokemon-image div{
            width: 240px;
        }
    }
</style>
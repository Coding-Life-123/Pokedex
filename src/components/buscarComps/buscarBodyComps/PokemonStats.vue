<script setup>
import { computed } from 'vue';


const props = defineProps({
    pokemonStats:Array,
    colors:Array
})

const stats = computed(()=> props.pokemonStats);
const colors = computed(()=> props.colors);


</script>

<template>
    <div 
      style="
        margin: 0 auto; 
        display: flex;
        flex-direction: column;
        justify-content: center;
        text-align: center;
        flex: 1;
        width: 30%;
        background-color: rgba(50, 50, 50, 0.65);
        backdrop-filter: blur(8px);
        padding: 20px;
        border-radius: 20px;
      ">
        <h3 style="margin: 0 auto;">Estadisticas</h3>
        <div v-for="(stat, i) in stats" :key="i" style="margin-top: 15px; display: flex; flex-direction: column; justify-content: center; gap: 10px;" >
            <p>{{stat.stat.name}} : {{ stat.base_stat }}/255</p>
            <div style="width: 100%; height: 20px; background-color: white; border-radius: 10px;">
                <div class="fill-bar" style="height: 20px; border-radius: 10px; transition: width 0.7s cubic-bezier(0.68, -0.55, 0.27, 1.55);"
                :style="{
                    width:`${(stat.base_stat/255)*100}%`,
                    background:`linear-gradient(160deg, ${colors[0]}, ${colors[1]})`,
                }"></div>
            </div>
        </div>
    </div>
</template>

<style>
</style>

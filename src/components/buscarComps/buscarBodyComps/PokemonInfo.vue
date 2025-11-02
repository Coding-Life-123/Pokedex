<script setup>
import axios from "axios";
import { computed, ref } from "vue";

const props = defineProps({
  pokemonIndex: Number,
  pokemonTypes: Array,
  pokemonStrong: Array,
  pokemonWeak: Array,
  colors: Array,
  colorsList: Object,
});

const pokemonId = computed(() => props.pokemonIndex);
const pokemonTypes = computed(() => props.pokemonTypes);
const strongList = computed(() => props.pokemonStrong);
const weakList = computed(() => props.pokemonWeak);
const colors = computed(() => props.colors);
const typeColors = props.colorsList;

const cleanStrongList = computed(()=>{
    const filtered = strongList.value.filter(strong => !weakList.value.includes(strong));
    return [...new Set(filtered)];
});

const cleanWeakList = computed(()=>{
    const filtered = weakList.value.filter(weak => !strongList.value.includes(weak));
    return [...new Set(filtered)];
});


</script>

<template>
  <div
    style="
      display: flex;
      flex-direction: column;
      justify-content: space-evenly;
      width: 30%;
      margin: 0 auto;
      text-align: center;
      background-color: rgba(50, 50, 50, 0.65);
      backdrop-filter: blur(8px);
      padding: 20px;
      border-radius: 20px;
      transition: color 1s ease;
    "
    :style="{
      color: `${colors[0]}`,
    }"
  >
    <h2 style="font-size: 60px">#{{ pokemonId }}</h2>
    <h3>Tipos del Pokémon:</h3>
    <div style="display: flex; justify-content: center; gap: 10px;">
      <p
        style="color: white; font-weight: 600; padding: 8px 10px; border-radius: 10px;"
        v-for="(type, index) in pokemonTypes"
        :key="index"
        :style="{backgroundColor:`${typeColors[type.value]}`}"
      >
        {{ type }}
      </p>
    </div>
    <h3>Debilidades:</h3>
    <div style="display: flex; gap: 10px; flex-wrap: wrap; justify-content: center;">
      <p 
        style="color: white; font-weight: 600; padding: 8px 10px; border-radius: 10px;"
        v-for="(weak, index) in cleanWeakList"
        :key="index"
        :style="{backgroundColor:`${typeColors[weak]}`}"
      >
        {{ weak }}
      </p>
    </div>
    <h3>Fortalezas:</h3>
    <div style="display: flex; gap: 10px; flex-wrap: wrap; justify-content: center;">
      <p 
        style="color: white; font-weight: 600; padding: 8px 10px; border-radius: 10px;"
        v-for="(strong, index) in cleanStrongList"
        :key="index"
        :style="{backgroundColor:`${typeColors[strong]}`}"
      >
        {{ strong }}
      </p>
    </div>
  </div>
</template>

<style></style>

<template>
  <div class="fondo">
    <div class="main-container">
      <PokemonImg :data="data"/>
      <div class="pokemon-info">

      </div>
      <div class="pokemon-stats">

      </div>
    </div>
  </div>
</template>

<script setup>
  import axios from 'axios';
  import { ref, defineEmits } from 'vue'
  import Pikachu from './buscarComps/Pikachu.vue';
  import PokemonImg from './buscarComps/PokemonImg.vue';

 
  const data = ref('');

  async function buscarPokemon(nombre="Pikachu"){
    const res = ref(await axios.get(`https://pokeapi.co/api/v2/pokemon/${nombre}`));
    data.value = res.value;
    
    console.log(data.value)
  }

  const emit = defineEmits(['pagina']);

  function volverMenu(){
    emit('pagina', 'Menu.vue');
  }

  buscarPokemon("lugia")
</script>

<style>


.pokemon-image{
  height: fit-content;
  width: fit-content;
}

.pokemon-image img{
  height: 500px;
  width: 500px;
}
</style>

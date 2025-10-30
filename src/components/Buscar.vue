<template>
  <div>
    <div class="main-container">
      <div class="pokemon">
        <img :src="imgSrc" alt="">
      </div>
    </div>
  </div>
</template>

<script setup>
  import axios from 'axios';
  import { ref, defineEmits } from 'vue'
  import Pikachu from './buscarComps/Pikachu.vue';

  const imgSrc = ref('')

  async function buscarPokemon(nombre="Pikachu"){
    const res = ref(await axios.get(`https://pokeapi.co/api/v2/pokemon/${nombre}`));
    console.log(res.value.data);
    imgSrc.value = res.value.data.sprites.front_default
    console.log(imgSrc.value)
  }

  const emit = defineEmits(['pagina']);

  function volverMenu(){
    emit('pagina', 'Menu.vue');
  }

  buscarPokemon("reshiram")
</script>

<style>

</style>

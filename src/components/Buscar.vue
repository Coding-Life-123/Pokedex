<template>

</template>

<script setup>
  import axios from 'axios';
  import { ref, defineEmits } from 'vue'

  async function buscarPokemon(nombre){
    let res = ref(await axios.get(`https://pokeapi.co/api/v2/pokemon/${nombre}`));
    console.log(res.value.data);
  }

  const emit = defineEmits(['pagina']);

  function volverMenu(){
    emit('pagina', 'menu');
  }

  buscarPokemon("pikachu")
</script>

<style scoped>

</style>

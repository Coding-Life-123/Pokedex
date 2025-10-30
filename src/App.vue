<script setup>
  import { ref } from 'vue';
  import Buscar from './components/Buscar.vue'
  import Menu from './components/Menu.vue';
  import Aleatorio from './components/Aleatorio.vue';

  const pagina = ref('Menu.vue')
  function recibirDato(pag){
    pagina.value = pag;
    console.log(`valor recibido: `+ pag);
  }
</script>

<template>
  <div>
    <Buscar v-if="pagina === 'Buscar.vue'" @pagina="recibirDato" />
    <Aleatorio v-else-if="pagina === 'Aleatorio.vue'" @pagina="recibirDato" />
    <Menu v-else-if="pagina === 'Menu.vue'" @pagina="recibirDato" />
  </div>
</template>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap');

  *{
    padding: 0px;
    margin: 0px;
    font-family: 'Orbitron', sans-serif;
  }

</style>

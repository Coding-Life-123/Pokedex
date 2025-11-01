<script setup>
  import axios from 'axios';
  import { ref, defineEmits } from 'vue'
  import Pikachu from './buscarComps/Pikachu.vue';
  import PokemonImg from './buscarComps/PokemonImg.vue';
import PokemonInfo from './buscarComps/PokemonInfo.vue';

 
  const data = ref(null);
  const colors = ref([]);
    const typeColors = {
    normal: "#A8A77A",
    fire: "#EE8130",
    water: "#6390F0",
    electric: "#F7D02C",
    grass: "#7AC74C",
    ice: "#96D9D6",
    fighting: "#C22E28",
    poison: "#A33EA1",
    ground: "#E2BF65",
    flying: "#A98FF3",
    psychic: "#F95587",
    bug: "#A6B91A",
    rock: "#B6A136",
    ghost: "#735797",
    dragon: "#6F35FC",
    dark: "#705746",
    steel: "#B7B7CE",
    fairy: "#D685AD",
  };

  const pikachuSearch = ref('/pikachuSearch-idle.png')
  console.log(pikachuSearch.value)

  async function buscarPokemon(nombre="Pikachu"){
    const res = ref(await axios.get(`https://pokeapi.co/api/v2/pokemon/${nombre}`));
    data.value = res.value;
    console.log(data.value);

    if(data.value.data.types.length == 2){    
      const type1 = ref(data.value.data.types[0].type.name)
      const type2 = ref(data.value.data.types[1].type.name)
      colors.value = [typeColors[type1.value], typeColors[type2.value]];
    }else{
      const type1 = ref(data.value.data.types[0].type.name)
      colors.value = [typeColors[type1.value], typeColors[type1.value]]
    }
    console.log(colors.value[0])
  }

  const searchText = ref('')
  const showAlert = ref(false)
  let alertTimeout = null

  function handleTyping(){
    clearTimeout(alertTimeout)
    showAlert.value = false

    alertTimeout = setTimeout(() => {
      if(searchText.value.trim() !== ''){
        showAlert.value=true

        setTimeout(() => {
          showAlert.value=false
        }, 4000);
      }
    }, (3000));
  }

  const emit = defineEmits(['pagina']);

  function volverMenu(){
    emit('pagina', 'Menu.vue');
  }

  buscarPokemon("250")
</script>

<template>
  <div class="fondo">
    <div class="main-container" style="padding: 50px;">
      <div class="head-container" 
      style="
        display: flex;
        width: 100%;
      ">
        <Pikachu style="margin:0; border-radius: 10px; position: fixed;"/>
        <form class="search-container" 
        @submit.prevent
        style="
          margin: auto;
          padding: none;
          display: flex;
          height: fit-content;
          position: relative;
          border-radius: 10px !important;
        ">
          <div 
          style="
          margin: auto;
          padding: 3px;
          border-radius: 10px;
          "
          :style="{
            background:`linear-gradient(135deg, ${colors[0]}, ${colors[1]})`
          }">
            <input type="text" placeholder="Encontrar Pokémon..."
            @input="handleTyping"
            v-model="searchText"
            style="
              margin: auto;
              height: 20px;
              padding: 5px 8px;
              font-family: 'Orbitron', sans-serif;
              border-radius: 10px;
              border: none;
            "
            :style="{
              }"
            >
          </div>
          <button 
          @mouseenter="pikachuSearch = '/pikachuSearch-hover.png'"
          @mouseleave="pikachuSearch = '/pikachuSearch-idle.png'"
          style="
            background-color: transparent;
            border: none;
            margin: auto;
            margin-left: 10px;
            height: 60px;
            overflow: hidden;
            cursor: pointer;
          ">
            <img :src="pikachuSearch" style="width: 50px;" alt="">
          </button>
          <transition name="fade">
            <div v-if="showAlert" class="alert" 
            style="
              position: absolute;
              bottom: 100%;
              left: 50%;
              transform: translateX(-50%) translateY(-2px);
              background-color: #fed400;
              color: black;
              padding: 8px 12px;
              border-radius: 8px;
              box-sizing: 0 2px 8px rgba(0,0,0,0.3);
              white-space: nowrap;
            ">
              Haz que pikachu busque a tú Pokémon!
            </div>
          </transition>
        </form>
      </div>
      <div class="body-container" 
      style="
        margin-top: 40px;
        display: flex;
      ">
        <PokemonImg 
          :data="data" 
          :colors="colors"
        />
        <PokemonInfo 
          :pokemonIndex="data.id" 
          :pokemonTypes="data.types" 
          :colors="colors"

        />
        <div class="pokemon-stats">

        </div>
      </div>
    </div>
  </div>
</template>

<style>

.fade-enter-active,
.fade-leave-active{
  transition: opacity 0.3s ease, transform 0.7s ease;
}

.fade-enter-from,
.fade-leave-to{
  opacity: 0;
  transform: translateY(5px);
}

.pokemon-image{
  height: fit-content;
  width: fit-content;
}

.pokemon-image img{
  margin: auto;
  height: 400px;
  width: 400px;
}
</style>

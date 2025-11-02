<script setup>
import Pikachu from "./buscarComps/buscarBodyComps/Pikachu.vue";
import BuscarBody from "./buscarComps/BuscarBody.vue";
import { ref, defineEmits, watch } from "vue";

const colors = ref([]);
function recibirColores(colorsArr) {
  colors.value = colorsArr;
}

const searchText = ref("mewtwo");
const pokemon = ref("mewtwo")
const showAlert = ref(false);
let alertTimeout = null;
const alertShown = ref(false);

const loading = ref(false)

function handleTyping() {
  if (alertShown.value == false) {
    clearTimeout(alertTimeout);
    showAlert.value = false;

    alertTimeout = setTimeout(() => {
      if (searchText.value.trim() !== "") {
        showAlert.value = true;

        setTimeout(() => {
          showAlert.value = false;
        }, 4000);
      }
    }, 3000);
    alertShown.value = true;
  }
}


const emit = defineEmits(["pagina"]);

const pikachuSearch = ref("/pikachuSearch-idle.png");

function volverMenu() {
  emit("pagina", "Menu.vue");
}
</script>

<template>
  <div class="fondo">
    <h1>Hola</h1>
    <div class="head-container" style="display: flex; width: 100%">
      <Pikachu style="margin: 0; border-radius: 10px; position: fixed" />
      <form
        class="search-container"
        @submit.prevent
        @submit="pokemon = searchText"
        style="
          margin: auto;
          padding: 0;
          display: flex;
          height: fit-content;
          position: relative;
          border-radius: 10px;
        "
      >
        <div style="margin: auto; padding: 3px; border-radius: 10px"
        :style="{
            background:`linear-gradient(135deg, ${colors[0]}, ${colors[1]})`
          }">        
          <input
            type="text"
            placeholder="Encontrar Pokémon..."
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
          />
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
          "
        >
          <transition name="fadePikachu">
            <img :src="pikachuSearch" style="width: 50px" alt="" />
          </transition>
        </button>
        <transition name="fade">
          <div
            v-if="showAlert"
            class="alert"
            style="
              position: absolute;
              bottom: 100%;
              left: 50%;
              transform: translateX(-50%) translateY(-2px);
              background-color: #fed400;
              color: black;
              padding: 8px 12px;
              border-radius: 8px;
              box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
              white-space: nowrap;
            "
          >
            Haz que pikachu busque a tú Pokémon!
          </div>
        </transition>
      </form>
    </div>
    <BuscarBody v-show="!loading" :key="'buscarBody'" @enviarDato="recibirColores" :pokemon="pokemon" />
    <h1 v-show="loading">Hola</h1>
  </div>
</template>

<style></style>

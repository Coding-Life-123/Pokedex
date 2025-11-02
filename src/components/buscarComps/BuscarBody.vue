<script setup>
import axios from "axios";
import { ref, defineEmits, watch, computed } from "vue";
import PokemonImg from "./buscarBodyComps/PokemonImg.vue";
import PokemonInfo from "./buscarBodyComps/PokemonInfo.vue";
import PokemonStats from "./buscarBodyComps/PokemonStats.vue";

const data = ref(null);
const strong = ref([]);
const weak = ref([]);
const pokemonId = ref(0);
const pokemonTypes = ref([]);
const colors = ref([]);
const stats = ref([]);
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

const props = defineProps({
  pokemon: String
})

buscarPokemon('mewtwo')

watch(() => props.pokemon,(newValue, oldValue)=>{
  console.log(`el pokémon cambió de ${oldValue} a ${newValue}`);

  if(newValue) buscarPokemon(newValue);
})

const emit = defineEmits(["enviarDato"]);

watch(colors, (newColors) => {
  emit("enviarDato", newColors);
});

async function buscarPokemon(nombre = "pikachu") {
  strong.value = [];
  weak.value = [];
  

  try{
    const res = await axios.get(`https://pokeapi.co/api/v2/pokemon/${nombre}`)
  
    data.value = res.data;

    stats.value = res.data.stats;

    console.log(data.value)
    console.log(stats.value)

    pokemonId.value = res.data.id;

    if (res.data.types.length == 2) {
      let type1 = res.data.types[0].type.name;
      let type2 = res.data.types[1].type.name;
      pokemonTypes.value = [type1, type2];
      colors.value = [typeColors[type1], typeColors[type2]];

      const type1Rels = await buscarRelaciones(type1);
      const type2Rels = await buscarRelaciones(type2);

      const doubleDmgTo = [
        ...type1Rels.double_damage_to,
        ...type2Rels.double_damage_to,
      ];
      doubleDmgTo.forEach((type) => strong.value.push(type.name));

      const doubleDmgFrom = [
        ...type1Rels.double_damage_from,
        ...type2Rels.double_damage_from,
      ];
      doubleDmgFrom.forEach((type) => weak.value.push(type.name));
    } else if (
      res.data.types.length === 1 &&
      res.data.types[0].type.name !== "normal"
    ) {
      let type1 = res.data.types[0].type.name;
      pokemonTypes.value = [type1];

      const type1Rels = await buscarRelaciones(type1);

      type1Rels.double_damage_to.forEach((type) =>
        strong.value.push(type.name)
      );
      type1Rels.double_damage_from.forEach((type) =>
        weak.value.push(type.name)
      );

      colors.value = [typeColors[type1], typeColors[type1]];
      console.log(strong);
    } else {
      console.log("este pokemon es tipo normal (snorlax seguramente)");
    }

    emit("enviarDato", colors);
  }catch(error){
    console.error("error al buscar Pokémon:", error)
    data.value = null;
    stats.value = [],
    pokemonId.value = 0;
    pokemonTypes.value = [];
    colors.value =[];
  }

  console.log(data.value);
  console.log(stats.value);
  console.log(pokemonId.value);
  console.log(pokemonTypes.value);
  console.log(colors.value);
}


async function buscarRelaciones(type) {
  try{
    const res = await axios.get(`https://pokeapi.co/api/v2/type/${type}`);
    return res.data.damage_relations;
  }catch(error){
    console.error("Error al buscar relaciones:", error);
    return { double_damage_to: [], double_damage_from: []};
  }
}

</script>

<template>
  <div>
    <div class="main-container" style="padding: 50px">
      <div
        class="body-container"
        style="margin-top: 100px; display: flex; width: 100%; gap: 30px"
      >
        <PokemonImg :data="data" :colors="colors" />
        <PokemonInfo
          :pokemonIndex="pokemonId"
          :pokemonTypes="pokemonTypes"
          :pokemonStrong="strong"
          :pokemonWeak="weak"
          :colors="colors"
          :colorsList="typeColors"
        />
        <PokemonStats :pokemonStats="stats" :colors="colors" />
      </div>
    </div>
  </div>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease, transform 0.7s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(5px);
}

.pokemon-image {
  height: fit-content;
  width: fit-content;
}

.pokemon-image img {
  margin: auto;
  width: 100%;
}
</style>

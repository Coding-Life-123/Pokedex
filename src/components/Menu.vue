<template>
    <div class="flex" style="height: 100vh;">
        <div class="margin-auto flex column">
            <div class="logo margin-auto">
                <img src="/pokeball.png" alt="">
            </div>
            <h1 class="margin-auto">POKÉDEX</h1>
            <div class="pages">
                <MenuCards :mensaje="'Busca un pokémon! ->'" @click="decidirPag('Buscar.vue')"/>
                <MenuCards :mensaje="'Descubre un pokémon! ->'" @click="decidirPag('Aleatorio.vue')"/>            
            </div>
        </div>
    </div>
</template>

<script setup>

    import { defineEmits } from 'vue';
    import MenuCards from './menuComps/MenuCards.vue';

    //lógica navegación
    const emit = defineEmits(['pagina']);

    function decidirPag(pag){
        emit('pagina', pag);
    }

</script>

<style>

*{
    margin: 0px;
}

.flex{
    display: flex;
}

.column{
    flex-direction: column;
}

.margin-auto{
    margin: auto;
}

.logo{
    width: fit-content;
    height: fit-content;
}

.logo img{
    width: 200px;
    height: 200px;
}

h1{
    font-size: 40px;
}

.pages{
    display: flex;
    justify-content: space-around;
    margin-top: 30px;
    width: 600px;
}

.pages div{
    width: fit-content;
}

</style>
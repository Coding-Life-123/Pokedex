<template>
    <div class="flex fondo">
        <div class="margin-auto flex column">
            <div class="logo margin-auto">
                <img src="/pokeball.png" alt="">
            </div>
            <h1 class="margin-auto">POKÉDEX</h1>
            <div class="pages">
                <div class="page-card">
                    <h3>Busca un pokémon!</h3>
                </div>
                <div class="page-card">
                    <h3>Descubre un Pokémon al azar!</h3>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
    import { ref, defineEmits } from 'vue';

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

.fondo{
    height: 100vh;
    color: white;
    background-image: url("/fondo.png");
    background-size: cover;
    background-position: center;
    background-attachment: fixed;
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

}



</style>
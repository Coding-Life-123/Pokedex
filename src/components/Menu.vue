<template>
    <div class="flex">
        <div class="margin-auto">
            <div class="logo margin-auto">
                <img src="/pokeball.png" alt="">
            </div>
            <h1 class="margin-auto">POKÉDEX</h1>
            <div class="pages">

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
    height: 100vh;
    color: white;
    background: radial-gradient(circle 30% 50%, rgb(255, 83, 83))/*(90deg, rgb(255, 83, 83) 0%, rgb(179, 0, 0) 20%,  rgb(179, 0, 0) 80%, rgb(255, 83, 83) 100%) */; 
    background-color: rgb(179, 0, 0);
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

</style>
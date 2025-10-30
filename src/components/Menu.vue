<template>
    <div class="flex fondo">
        <div class="margin-auto flex column">
            <div class="logo margin-auto">
                <img src="/pokeball.png" alt="">
            </div>
            <h1 class="margin-auto">POKÉDEX</h1>
            <div class="pages">
                <div class="page-card" 
                @mousemove="moverCursor"
                @mouseleave="reiniciarCursor"
                :style="{'--x': x + 'px', '--y': y + 'px'}"
                >
                    <h3>Busca un pokémon! -></h3>
                </div>
                <div class="page-card"
                @mousemove="moverCursor"
                @mouseleave="reiniciarCursor"
                :style="{'--x': x + 'px', '--y': y + 'px'}"
                >
                    <h3>Descubre un Pokémon! -></h3>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
    import { ref, defineEmits } from 'vue';

    //lógica estilo mouse
    const x = ref(150);
    const y = ref(75);

    function moverCursor(e){
        const rect = e.target.getBoundingClientRect();
        x.value = e.clientX - rect.left;
        y.value = e.clientY - rect.top;
    }

    function reiniciarCursor(e){
        x.value = 150;
        y.value = 75;
    }

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
    column-gap: 5%;
    margin-top: 30px;
    width: 600px;
}

.page-card{
    background: linear-gradient(135deg, #ff4b2b 10%, #b31217 90%);
    height: 50px;
    width: 50%;
    padding: 10px 10px;
    border-radius: 10px;
    display: flex;
    cursor: pointer;
    transition: 0.3s ease;
    text-align: justify;


    
    h3{
        margin: auto;
    }
}

.page-card::before{
    content: "";
    position: absolute;
    top: var(--y, 50%);
    left: var(--x, 50%);
    transform: translate(-50%, -50%);
    width: 250%;
    height: 250%;
    background: radial-gradient(circle at center, rgba(255, 50, 50, 0.3), transparent 60%);
    pointer-events: none;
    opacity: var(--visible, 0);
    transition: opacity 0.3s ease, top 0.05s linear, left 0.05s linear;
}

.page-card:hover{
    transform: scale(1.08);
    transition: 0.3s ease;
    color: rgb(255, 255, 255);
}




</style>

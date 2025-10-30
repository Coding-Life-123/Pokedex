<template>
    <div>
        <div class="page-card"
        @mousemove="moverCursor"
        @mouseenter="hovered = true"
        @mouseleave="hovered = false"
        :style="{'--x': x + 'px', '--y': y + 'px', '--visible': hovered ? 1 : 0}"
        >
            <h3>{{ props.mensaje }}</h3>
        </div>
    </div>
</template>

<script setup>
    import { ref, defineEmits } from 'vue';

    //lógica estilo mouse
    const x = ref(150);
    const y = ref(75);

    const hovered = ref(false)

    const props = defineProps({
        mensaje: String
    })

    function moverCursor(e){
        const rect = e.target.getBoundingClientRect();
        x.value = e.clientX - rect.left;
        y.value = e.clientY - rect.top;
        console.log(x, y);
    }
</script>

<style>
    .page-card{
        background: #ff6a3d /*linear-gradient(135deg, #ff6a3d 10%, #d72638 90%)*/;
        height: 50px;
        width: 100%;
        margin: auto;
        padding: 10px 10px;
        border-radius: 10px;
        display: flex;
        flex-direction: column;
        cursor: pointer;
        text-align: justify;
        position: relative;
        overflow: hidden;
        color: white;
        transition: 0.3s ease;
        box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);

        h3{
            margin: auto;
            z-index: 20;
        }
    }

    .page-card::before{
        content: "";
        position: absolute;
        top: var(--y,S 50%);
        left: var(--x, 50%);
        transform: translate(-50%, -50%);
        width: 250%;
        height: 250%;
        background: radial-gradient(circle at center, #d72638 0%, transparent 60%);
        pointer-events: none;
        transform: 0.05s linear;
        z-index: 10;
        opacity: var(--visible, 0);
    }

    .page-card:hover{
        transform: scale(1.08);
        transition: 0.3s ease;
        color: rgb(255, 255, 255);
        box-shadow: 0 0 40px #d72638;
        width: 100%;
    }
</style>
<template>
    <div>
        <img :src="estadoActual" style="width: 100px; border-radius: 10px;" alt="">
    </div>
</template>

<script setup>
    import { ref, watch } from 'vue';

    const gifs = {
        idle:"",
        happy:"happy1.png"
    }

    const estadoActual = ref(gifs.happy);
</script>

<style></style>
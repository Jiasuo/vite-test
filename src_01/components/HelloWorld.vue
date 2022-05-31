<script setup>
    import gsap from "gsap"
import { onMounted } from "vue";
    onMounted(() =>{
        gsap.from("#hello", {y: "50vw", opacity:0})
    })
</script>

<template>
    <div id="hello">Hello world</div>
</template>

<style scoped>
    #hello{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
</style>
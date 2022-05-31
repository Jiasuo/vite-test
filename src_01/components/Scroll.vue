<script setup>
import {gsap} from "gsap"
import {ScrollTrigger} from "gsap/ScrollTrigger"
import { onBeforeUnmount, onMounted, ref } from "vue";
gsap.registerPlugin(ScrollTrigger)

const d1 = ref(null);
const d2 = ref(null)
const d3 = ref(null)

onMounted(() => {
    gsap.from(d2.value, {
        scrollTrigger: {
            trigger: d2.value,
            toggleActions: "restart pause reverse pause",
            start: "top center",
            end: ".block.d3",
            scrub: 2,
            pin: true,
            markers: true
        },
        backgroundColor: "#000",
        duration: 2,
        // ease: "bounce",
    })
    gsap.ticker.add(showFrame)
})

onBeforeUnmount(() => {
    gsap.ticker.remove(showFrame)
})

function showFrame(_, elapsed, frame){
    console.log(`[${frame}]: ${elapsed}ms`);
}
</script>

<template>
    <div class="block d1">
        <div ref="d1">Hello</div>
    </div>
    <div class="block d2">
        <div ref="d2">I'm</div>
    </div>
    <div class="block d3">
        <div ref="d3">Jack</div>
    </div>
</template>

<style scoped>
.block {
    height: 100vh;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 32px;
    font-family: "Roboto", sans-serif;
    font-weight: bold;
}

.d1 {
    background-color: blue;
}

.d2 {
    background-color: orange;
}

.d3 {
    background-color: green;
}
</style>
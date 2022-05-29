<script setup>
import { reactive, computed, ref, onMounted, onBeforeUnmount, watchEffect } from 'vue';

const L = ref(null), M = ref(null), S = ref(null)

const currentSize = ref('L')

const screenSize = reactive({
    l: 1920,
    m: 820,
    s: 412
})
const size = reactive({
    l: 0,
    m: 0,
    s: 0
})
const result = computed(() => {
    return {
        l: (Math.round(size.l / (screenSize.l / 100) * 100) / 100) || 0,
        m: (Math.round(size.m / (screenSize.m / 100) * 100) / 100) || 0,
        s: (Math.round(size.s / (screenSize.s / 100) * 100) / 100) || 0,
    }
})

function changeInputSize(e) {
    e.target.style.width = e.target.value.length + 'ch';
}

onMounted(() => {
    // Resize inputs to fit content
    const inputs = document.querySelectorAll('input');
    inputs.forEach((i) => {
        i.style.width = i.value.length + 'ch'
        i.addEventListener('input', changeInputSize)
    })
})

onBeforeUnmount(() => {
    const inputs = document.querySelectorAll('input');
    inputs.forEach((i) => {
        i.removeEventListener('input', changeInputSize)
    })
})

watchEffect(() => {
    if (currentSize.value === 'L' && result.value.l !== 0) {
        navigator.clipboard.writeText(`${result.value.l}vw`);
    } else if (currentSize.value === 'M' && result.value.m !== 0) {
        navigator.clipboard.writeText(`${result.value.m}vw`);
    } else {
        if(result.value.s !== 0){
            navigator.clipboard.writeText(`${result.value.s}vw`);
        }
    }
})
</script>

<template>
    <div class="container">
        <div class="vw l">
            <div class="screenWidth">
                <h1>Large</h1>
                Screen width: <input type="number" v-model="screenSize.l"
                    @focus="currentSize = 'L'; $event.target.select()"> px
            </div>
            <div class="width">Size: <input type="number" v-model="size.l" ref="L"
                    @focus="currentSize = 'L'; $event.target.select()"> px</div>
            <div class="result">{{ result.l }}vw</div>
        </div>
        <div class="vw m">
            <div class="screenWidth">
                <h1>Medium</h1>
                Screen width: <input type="number" v-model="screenSize.m"
                    @focus="currentSize = 'M'; $event.target.select()"> px
            </div>
            <div class="width">Size: <input type="number" v-model="size.m" ref="M"
                    @focus="currentSize = 'M'; $event.target.select()"> px</div>
            <div class="result">{{ result.m }}vw</div>
        </div>
        <div class="vw s">
            <div class="screenWidth">
                <h1>Small</h1>
                Screen width: <input type="number" v-model="screenSize.s"
                    @focus="currentSize = 'S'; $event.target.select()"> px
            </div>
            <div class="width">Size: <input type="number" v-model="size.s" ref="S"
                    @focus="currentSize = 'S'; $event.target.select()"> px</div>
            <div class="result">{{ result.s }}vw</div>
        </div>
    </div>
</template>

<style scoped>
.container {
    height: 100vh;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    text-align: center;
    font-family: "Roboto", sans-serif;
    font-size: 1.5vw;
}

h1 {
    font-size: 2vw;
    font-weight: 700;
}

.vw {
    /* height: 100%; */
    /* padding: 1vw;
    border-radius: 2vw; */
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: white;
}

.vw.l {
    background-image: linear-gradient(155deg,
            hsl(67deg 100% 60%) 0%,
            hsl(59deg 100% 46%) 11%,
            hsl(53deg 100% 46%) 22%,
            hsl(47deg 100% 46%) 33%,
            hsl(41deg 100% 46%) 44%,
            hsl(36deg 100% 45%) 56%,
            hsl(30deg 100% 44%) 67%,
            hsl(24deg 100% 42%) 78%,
            hsl(17deg 100% 41%) 89%,
            hsl(6deg 97% 39%) 100%);
}

.vw.m {
    background-image: linear-gradient(155deg,
            hsl(125deg 87% 60%) 0%,
            hsl(151deg 100% 44%) 11%,
            hsl(163deg 100% 39%) 22%,
            hsl(176deg 100% 35%) 33%,
            hsl(188deg 100% 35%) 44%,
            hsl(196deg 100% 35%) 56%,
            hsl(202deg 100% 32%) 67%,
            hsl(206deg 100% 28%) 78%,
            hsl(210deg 100% 23%) 89%,
            hsl(215deg 98% 17%) 100%);
}

.vw.s {
    background-image: linear-gradient(155deg,
            hsl(358deg 85% 55%) 0%,
            hsl(344deg 100% 47%) 11%,
            hsl(339deg 100% 47%) 22%,
            hsl(334deg 100% 47%) 33%,
            hsl(328deg 100% 45%) 44%,
            hsl(320deg 100% 43%) 56%,
            hsl(309deg 100% 39%) 67%,
            hsl(294deg 100% 37%) 78%,
            hsl(277deg 100% 42%) 89%,
            hsl(247deg 80% 53%) 100%);
}

.result {
    font-size: 2vw;
    font-weight: 700;
    color: white;
    margin-top: 1.5vw;
}

input {
    margin-top: 2vw;
    font-family: "Roboto", sans-serif;
    border: white;
    background-color: transparent;
    text-align: right;
    padding: 0;
    outline: none;
    font-size: 1.5vw;
    font-weight: 700;
}

/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

/* Firefox */
input[type=number] {
    -moz-appearance: textfield;
}

::selection{
    background-color: white;
    color: #00b500
}

@media screen and (max-width: 991px) {
    .container {
        grid-template-columns: repeat(1, 1fr);
        grid-template-rows: repeat(3, 1fr);
        font-size: 2vw;
    }
    input{
        font-size: 2vw;
    }

    h1, .result {
        font-size: 4vw;
    }
}
@media screen and (max-width: 768px) {
    .container {
        grid-template-columns: repeat(1, 1fr);
        grid-template-rows: repeat(3, 1fr);
        font-size: 3vw;
    }
    input{
        font-size: 3vw;
    }

    h1, .result {
        font-size: 6vw;
    }
}
</style>
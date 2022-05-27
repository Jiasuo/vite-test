<script setup>
import {onMounted} from "vue"
import gsap from "gsap"
onMounted(() => {
  gsap.from("#target", {x:-100})
})
</script>

<template>
<div id="target">Hello world</div>
</template>

<style>
</style>

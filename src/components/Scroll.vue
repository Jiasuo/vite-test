<script setup>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { onMounted } from "vue";

onMounted(() => {
  gsap.registerPlugin(ScrollTrigger);
  gsap.utils.toArray("section").forEach(p => {
    ScrollTrigger.create({
      animation:gsap.to(p, {xPercent: -100, scaleX: 0}),
      trigger: p,
      start: "top top",
      scrub: true,
      pin: true,
      pinSpacing: false
    })
  })
});

</script>

<template>
  <section class="s1">1</section>
  <section class="s2">2</section>
  <section class="s3">3</section>
  <section class="s4">4</section>
</template>

<style scoped>
  section{
    overflow-x: hidden;
    height: 100vh;
    font-size: 120px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .s1{
    background: green;
  }
  .s2{
    background-color: red;
  }
  .s3{
    background-color: blue;
  }

  .s4{
    background-color: orange;
  }
</style>

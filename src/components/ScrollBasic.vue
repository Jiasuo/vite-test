<script setup>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { onMounted } from "vue";

onMounted(() => {
  gsap.registerPlugin(ScrollTrigger);
  ScrollTrigger.defaults({
    markers: true,
  });
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: ".square",
      // start: 100, // Absolute scrollX pixels
      start: "top 80%", // Top of the trigger Element reaches the center of viewport
      end: "600px 20%",
      scrub: 3,
      pin: true,
    },
  });
  tl.to(".square", {
    xPercent: 1000,
    duration: 8,
  });
  tl.to(".square", {
    y: "-100vh",
    duration: 4
  }, "-=4")
});
</script>

<template>
  <div class="div1"></div>
  <div class="div2">
    <div class="square"></div>
    <!-- <div class="square2"></div> -->
  </div>
</template>

<style scoped>
.div1,
.div2 {
  height: 100vh;
}

.div1 {
  background-color: pink;
}

.div2 {
  background-color: salmon;
}

.square {
  width: 100px;
  height: 100px;
  background-color: fuchsia;
}

/* .square2 {
    margin-top: 300px;
    width: 100px;
    height: 100px;
    background-color: blue;
} */
.active {
  background-color: white;
}
</style>

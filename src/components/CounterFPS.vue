<script setup lang="ts">
import { ref } from "vue";
const fps = ref("");
const minFps = ref("100");
// const fps = document.getElementById('fps')
let startTime = Date.now();
let frame = 0;

function tick() {
  const time = Date.now();
  frame++;
  if (time - startTime > 1000) {
    fps.value = (frame / ((time - startTime) / 1000)).toFixed(1);
    minFps.value =
      parseFloat(minFps.value) > parseFloat(fps.value)
        ? fps.value
        : minFps.value;
    startTime = time;
    frame = 0;
  }
  window.requestAnimationFrame(tick);
}
tick();
</script>

<template>
  <div style="padding: 0.5em">
    Estimated render speed: {{ fps }} FPS
    <span :style="parseFloat(minFps) < 30 ? 'color:red' : ''">
      (min {{ minFps }})</span
    >
  </div>
</template>

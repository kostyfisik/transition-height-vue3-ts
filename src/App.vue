<template>
  <div class="container mx-auto max-w-md p-4">
    <h1>Transition to height auto with Vue.js</h1>
    <div>Render speed: {{ fps }} FPS </div>
    <button
      class="bg-blue hover:bg-blue-dark text-white font-bold py-2 px-4 rounded mt-4"
      @click="expanded = !expanded"
    >
      {{ expanded ? `Shrink` : `Expand` }}
    </button>

    <div class="mt-8">
      Lorem ipsum dolor sit amet, consetetur sadipscing elitr,
      sed diam nonumy eirmod tempor invidunt ut labore et dolore.
    </div>
    <transition-expand>
      <div v-if="expanded">
        Magna aliquyam erat, sed diam voluptua. At vero eos et
        accusam et justo duo dolores et ea rebum. Stet clita kasd
        gubergren, no sea takimata sanctus est Lorem ipsum dolor
        sit amet. Lorem ipsum dolor sit amet, consetetur
        sadipscing elitr, sed diam nonumy eirmod tempor invidunt
        ut labore et dolore magna aliquyam erat, sed diam
        voluptua. At vero eos et accusam et justo duo dolores et
        ea rebum. Stet clita kasd gubergren, no sea takimata
        sanctus est Lorem ipsum dolor sit amet.
      </div>
    </transition-expand>
    <div class="mt-8">
      Lorem ipsum dolor sit amet, consetetur sadipscing elitr,
      sed diam nonumy eirmod tempor invidunt ut labore et dolore.
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import TransitionExpand from './components/TransitionExpand.vue'
// https://github.com/vueuse/head
// you can use this to manipulate the document head in any components,
// they will be rendered correctly in the html results with vite-ssg
useHead({
  title: 'Height (auto) transition example with Vue 3',
  meta: [
    { name: 'description', content: 'Height (auto) transition example with Vue 3' },
  ],
})

const fps = ref('')
// const fps = document.getElementById('fps')
let startTime = Date.now()
let frame = 0

function tick() {
  const time = Date.now()
  frame++
  if (time - startTime > 1000) {
    fps.value = ((frame / ((time - startTime) / 1000)).toFixed(1))
    startTime = time
    frame = 0
  }
  window.requestAnimationFrame(tick)
}
tick()

const expanded = ref(true)

// export default {
//   name: `App`,
//   components: {
//     TransitionExpand,
//   },
//   data() {
//     return {
//       expanded: false,
//     };
//   },
// };
</script>

<style>
.expand-enter-active,
.expand-leave-active {
  transition-property: opacity, height;
}

.expand-enter,
.expand-leave-to {
  opacity: 0;
}
</style>

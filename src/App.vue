
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

const expandedAll = ref(false)
const expandedOne = ref(false)

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

<template>
  <div class="container mx-auto max-w-md p-4">
    <h1>Transition to height auto with Vue.js</h1>
    <div>Estimated render speed: {{ fps }} FPS </div>
    <br>
    <button
      @click="expandedOne = !expandedOne"
    >
      {{ expandedOne ? `Shrink 2 elements` : `Expand 2 elements` }}
    </button>

    <button
      @click="expandedAll = !expandedAll"
    >
      {{ expandedAll ? `Shrink 100 elements` : `Expand 100 elements` }}
    </button>

    <div class="mt-8">
        Separator text... short element.
    </div>
    <transition-expand>
      <div v-if="expandedOne" style="background-color: rgb(0, 88, 4);">
        Magna aliquyam erat, sed diam voluptua.
      </div>
    </transition-expand>
    <div class="mt-8">
        Separator text... long element.
    </div>
    <transition-expand>
      <div v-if="expandedOne" style="background-color: rgb(0, 88, 4);">
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

    <div v-for="index in 100" :key="index">
      <div class="mt-8">
        Separator text...
      </div>
      <transition-expand>
        <div v-if="expandedAll" style="background-color:  rgb(0, 88, 4);">
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
        Separator text...
      </div>
    </div>
  </div>
</template>

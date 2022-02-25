<script setup lang="ts">
import { ref } from "vue";
import BasicExample from "./components/BasicExample.vue";
import CounterFPS from "./components/CounterFPS.vue";
import TransitionHeight from "../TransitionHeight.vue";
// https://github.com/vueuse/head
// you can use this to manipulate the document head in any components,
// they will be rendered correctly in the html results with vite-ssg
useHead({
  title: "Height (auto) transition demo with Vue3",
  meta: [
    {
      name: "description",
      content: "Height (auto) transition demo with Vue3",
    },
  ],
});
const basicToggle = ref(true);
const duration = ref(250);
</script>

<template>
  <div>
    <h1>
      Height (auto) transition demo with Vue3, TypeScript, and Web Animation API
    </h1>
    <a href="https://github.com/kostyfisik/transition-height-vue3-ts/blob/main/TransitionHeight.vue">GitHub</a>
    <CounterFPS />

    <button
      @click="duration == 250 ? (duration = 1000) : (duration = 250)"
      style="width: 10em; padding: 0.5em; margin: 0em 1em 1em 0em"
    >
      {{ duration == 250 ? `Increase` : `Decrease` }} animation duration
    </button>
    Current = {{ duration }} ms
    <br />

    <button @click="basicToggle = !basicToggle">
      {{ basicToggle ? `Hide basic example` : `Show basic example` }} (v-show)
    </button>
    <TransitionHeight :duration="duration">
      <div v-show="basicToggle">
        <BasicExample :duration="duration" />
      </div>
    </TransitionHeight>
    <div>Some final text...</div>
  </div>
</template>

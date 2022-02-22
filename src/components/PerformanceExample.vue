<script setup lang="ts">
import { ref } from "vue";
import TransitionHeight from "../../TransitionHeight.vue";
import CounterFPS from "./CounterFPS.vue";

interface Props {
  duration?: number;
}

const props = withDefaults(defineProps<Props>(), {
  duration: 250,
});

const totalCount = ref(25);

const expandedAll = ref(false);
const expandedSeparatorText = ref(false);
</script>

<template>
  <div style="background-color: #2f4258">
    <h2>Check animation performance</h2>
    <CounterFPS style="background-color: #263546" />
    <button @click="expandedAll = !expandedAll" class="m-05em">
      {{
        expandedAll
          ? `Shrink ` + totalCount + ` elements`
          : `Expand ` + totalCount + ` elements`
      }}
      (v-if)
    </button>

    <button
      @click="expandedSeparatorText = !expandedSeparatorText"
      class="m-05em"
      style="margin: 1em 1em 1em 1em; padding: 0.5em"
    >
      {{
        expandedSeparatorText ? `Shrink repeated text` : `Expand repeated text`
      }}
    </button>
    <div>
      Using {{ totalCount }} elements
      <button
        @click="totalCount == 25 ? (totalCount = 100) : (totalCount = 25)"
        class="m-05em"
      >
        Toggle
      </button>
    </div>
    <div>
      On my laptop the combo of short animation time (250ms), expended 'Lorem
      impsum...' text, and expansion of repeated text sometimes skips animation
      completly :( However, height animation of {{ totalCount }} elements is a
      bad idea, as soon as the position of the last element is effected by
      contiously changing height of previous {{ totalCount - 1 }} elements.
      However, shrinking of the same elements seems to work fine... Finially,
      this is only the Chrome browser problem, Firefox works fine in any case.
    </div>
    <div v-for="index in totalCount" :key="index">
      <TransitionHeight :duration="props.duration">
        <div v-show="expandedAll" style="background-color: rgb(0, 88, 4)">
          <TransitionHeight :duration="props.duration">
            <div
              v-show="expandedSeparatorText"
              style="background-color: rgb(19, 122, 24)"
            >
              Text from nested transition... (v-show inside v-show)
            </div>
          </TransitionHeight>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
          eiusmod tempor incididunt ut labore et dolore magna aliqua. Magna
          aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo
          dolores et ea rebum. Stet clita kasd gubergren, no sea takimata
          sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet,
          consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut
          labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos
          et accusam et justo duo dolores et ea rebum. Stet clita kasd
          gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.
        </div>
      </TransitionHeight>
      <TransitionHeight :duration="props.duration">
        <div v-show="expandedSeparatorText">Separator text...</div>
      </TransitionHeight>
    </div>
  </div>
</template>

<style scoped>
.m-05em {
  margin: 0.5em 0.5em 0.5em 0.5em;
}
</style>

<script setup lang="ts">
import { ref } from "vue";
import TransitionHeight from "../../TransitionHeight.vue";
interface Props {
  duration?: number;
}

const props = withDefaults(defineProps<Props>(), {
  duration: 250,
});

const expandedAll = ref(true);
const expandedOne = ref(true);
const expandedPresetHeight = ref(true);
const expandedSeparatorText = ref(false);
</script>

<template>
  <div style="background-color: #2f4258">
    <button
      @click="expandedPresetHeight = !expandedPresetHeight"
      class="m-05em"
      style="padding: 0.5em"
    >
      {{ expandedPresetHeight ? `Shrink with classes` : `Expand with classes` }}
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

    <button @click="expandedOne = !expandedOne" class="m-05em">
      {{ expandedOne ? `Shrink 2 elements` : `Expand 2 elements` }} (v-show)
    </button>

    <button @click="expandedAll = !expandedAll" class="m-05em">
      {{ expandedAll ? `Shrink 100 elements` : `Expand 100 elements` }} (v-if)
    </button>

    <div class="mt-8"> Separator text... height container. </div>
    <TransitionHeight :duration="props.duration">
      <div v-if="expandedPresetHeight" class="container--height">
        Using height container
      </div>
    </TransitionHeight>

    <div class="mt-8"> Separator text... height container with hidden overflow. </div>
    <TransitionHeight :duration="props.duration">
      <div v-if="expandedPresetHeight" class="container--height" style="overflow: hidden; height: 2em;">
        Text overflow when using height container. Magna aliquyam erat, sed diam
        voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet
        clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit
        amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam
        nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat,
        sed diam voluptua. At vero eos et accusam et justo duo dolores et ea
        rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem
        ipsum dolor sit amet.
      </div>
    </TransitionHeight>

    <div class="mt-8"> Separator text... padding-border-margin container. </div>
    <TransitionHeight :duration="props.duration">
      <div v-if="expandedPresetHeight" class="container--full-box">
        Using container with padding-border-margin settings
      </div>
    </TransitionHeight>

    <div class="mt-8"> Separator text... short element. </div>
    <TransitionHeight :duration="props.duration">
      <div v-show="expandedOne" style="background-color: rgb(0, 88, 4)">
        Magna aliquyam erat, sed diam voluptua.
      </div>
    </TransitionHeight>
    <div class="mt-8"> Separator text... long element. </div>
    <TransitionHeight :duration="props.duration">
      <div v-if="expandedOne" style="background-color: rgb(0, 88, 4)">
        Magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo
        duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata
        sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet,
        consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut
        labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et
        accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no
        sea takimata sanctus est Lorem ipsum dolor sit amet.
      </div>
    </TransitionHeight>

    <div v-for="index in 100" :key="index">
      <TransitionHeight :duration="props.duration">
        <div v-if="expandedAll" style="background-color: rgb(0, 88, 4)">
          Magna aliquyam erat, sed diam voluptua. At vero eos et accusam et
          justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea
          takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit
          amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor
          invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua.
          At vero eos et accusam et justo duo dolores et ea rebum. Stet clita
          kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit
          amet.
          <TransitionHeight :duration="props.duration">
            <div v-show="expandedSeparatorText" class="mt-8" style="  background-color: rgb(19, 122, 24);">
              Text from nested transition... (v-show inside v-if)
            </div>
          </TransitionHeight>
        </div>
      </TransitionHeight>
      <TransitionHeight :duration="props.duration">
        <div v-if="expandedSeparatorText" class="mt-8"> Separator text... </div>
      </TransitionHeight>
    </div>
  </div>
</template>

<style scoped>
.container--full-box {
  background-color: rgb(0, 88, 4);
  width: 10em;
  padding-bottom: 1em; /* 1:1 Aspect Ratio */
  padding-top: 1em; /* 1:1 Aspect Ratio */
  margin-top: 1em;
  margin-bottom: 1em;
  border-top: 1em solid black;
  border-bottom: 1em solid black;
  position: relative; /* If you want text inside of it */
}

.container--height {
  background-color: rgb(0, 88, 4);
  height: 5em;
}

.m-05em {
  margin: 0.5em 0.5em 0.5em 0.5em;
}
</style>

<script setup lang="ts">
import { ref } from "vue";
import TransitionHeight from "../../TransitionHeight.vue";
import PerformanceExample from "./PerformanceExample.vue";
interface Props {
  duration?: number;
}

const props = withDefaults(defineProps<Props>(), {
  duration: 250,
});

const expandedOne = ref(true);
const expandedPresetHeight = ref(true);
</script>

<template>
  <div style="background-color: #2f4258" class="pl-05em">
    <button
      @click="expandedPresetHeight = !expandedPresetHeight"
      class="m-05em"
      style="padding: 0.5em"
    >
      {{ expandedPresetHeight ? `Shrink with classes` : `Expand with classes` }}
    </button>
    <button
      @click="expandedOne = !expandedOne"
      class="m-05em"
      style="margin-top: 1em"
    >
      {{ expandedOne ? `Shrink 2 elements` : `Expand 2 elements` }} (v-show)
    </button>

    <div class="m-05em">
      Using distinct margin-top for buttons above... shouldn't be a problem for
      the parent height transition
    </div>

    <h2>Extended style example</h2>
    <button
      @click="expandedPresetHeight = !expandedPresetHeight"
      class="m-05em"
      style="padding: 0.5em"
    >
      {{ expandedPresetHeight ? `Shrink with classes` : `Expand with classes` }}
    </button>

    <div class="pl-05em">
      <span style="font-weight: bolder">
        This transition uses overflow:hidden during the animation.
      </span>
      See some possible styling conflict with ::before CSS selector from the
      following div in action.
    </div>
    <TransitionHeight :duration="props.duration">
      <p v-if="expandedPresetHeight" class="container--height">
        Using height container in &lt;p&gt; tag
      </p>
    </TransitionHeight>

    <div>&lt;div&gt; container with given height and hidden overflow.</div>
    <TransitionHeight :duration="props.duration">
      <div
        v-if="expandedPresetHeight"
        class="container--height"
        style="overflow: hidden; height: 2.2em"
      >
        Text overflow when using height container. Magna aliquyam erat, sed diam
        voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet
        clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit
        amet.
      </div>
    </TransitionHeight>
    <div>Padding-border-margin &lt;div&gt; container.</div>
    <TransitionHeight :duration="props.duration">
      <div v-show="expandedPresetHeight" class="container--full-box">
        Using container with padding-border-margin settings
      </div>
    </TransitionHeight>

    <h2>Same visual animation duration</h2>

    <button @click="expandedOne = !expandedOne" class="m-05em">
      {{ expandedOne ? `Shrink 2 elements` : `Expand 2 elements` }} (v-show)
    </button>
    <div>Note, this transition is only for 'display:block' element. Short span element with jumping tail...</div>
    before span
    <TransitionHeight :duration="props.duration">
      <span v-show="expandedOne" style="background-color: rgb(0, 88, 4)">
        Magna aliquyam erat, sed diam voluptua.
      </span>
    </TransitionHeight>
    after span
    <div>Short element.</div>
    <TransitionHeight :duration="props.duration">
      <div v-show="expandedOne" style="background-color: rgb(0, 88, 4)">
        Magna aliquyam erat, sed diam voluptua.
      </div>
    </TransitionHeight>
    <div>Long element.</div>
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
    <PerformanceExample :duration="props.duration" />
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

.container--height::before {
  content: "::before selector";
  background-color: rgba(216, 214, 215, 0.2);
  border: 3px solid rebeccapurple;
  padding-top: 2.65em;
  /* padding-left: 2em; */
}

.m-05em {
  margin: 0.5em 0.5em 0.5em 0.5em;
}
.pl-05em>div,
.pl-05em>h2 {
  padding: 0em 0em 0em 0.5em;
}
</style>

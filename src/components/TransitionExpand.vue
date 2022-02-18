<script setup lang="ts">
// import { defineComponent } from 'vue'
const duration = 1250;

function prepareElement(element: HTMLElement) {
  const { width } = getComputedStyle(element);
  element.style.width = width;
  element.style.position = "absolute";
  element.style.visibility = "hidden";
  element.style.height = "";

  const { height } = getComputedStyle(element);
  element.style.width = "";
  element.style.position = "";
  element.style.visibility = "";
  element.style.height = "0px";
  element.style.overflow = "hidden";
  return height;
}

function animateTransition(
  element: HTMLElement,
  done: () => void,
  keyframes: Keyframe[] | PropertyIndexedKeyframes | null,
  options?: number | KeyframeAnimationOptions
) {
  const animation = element.animate(keyframes, options);
  // Set height to 'auto' to keep UI adaptivity
  element.style.height = "";
  animation.onfinish = () => {
    element.style.overflow = "";
    done();
  };
}

function enterTransition(element: Element, done: () => void) {
  const HTMLElement = element as HTMLElement;
  const height = prepareElement(HTMLElement);
  const keyframesEnter = [
    { height: "0px", opacity: "0" },
    { height, opacity: "1" },
  ];
  const optionsEnter = { duration, easing: "ease-in-out" };
  animateTransition(HTMLElement, done, keyframesEnter, optionsEnter);
}

function leaveTransition(element: Element, done: () => void) {
  const HTMLElement = element as HTMLElement;
  const { height } = getComputedStyle(HTMLElement);
  HTMLElement.style.height = height;
  HTMLElement.style.overflow = "hidden";

  const keyframes = [
    { height, opacity: "1" },
    { height: "0px", opacity: "0" },
  ];
  const options = { duration, easing: "ease-in-out" };

  const animation = HTMLElement.animate(keyframes, options);
  animation.onfinish = () => {
    // Set height to 'auto' to keep UI adaptivity
    HTMLElement.style.height = "";
    HTMLElement.style.overflow = "";
    done();
  };
}
</script>

<template>
  <Transition :css="false" @enter="enterTransition" @leave="leaveTransition">
    <slot />
  </Transition>
</template>

<style scoped>
* {
  will-change: height;
}
</style>

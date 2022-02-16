<template>
  <Transition name="expand" @enter="enter" @leave="leave" @after-enter="afterEnter">
    <slot />
  </Transition>
</template>

<script lang="ts">
// eslint-disable-next-line @typescript-eslint/ban-ts-comment
// @ts-nocheck
/* eslint-disable no-console */
import { defineComponent, ref } from 'vue'
export default defineComponent({
  name: 'TransitionExpand',
  setup() {
    const show = ref(false)
    return {
      show,
      afterEnter(element: Element) {
        console.log('after enter', element);

        (element as HTMLElement).style.height = ''
      },
      enter(element: Element) {
        const { height3 } = getComputedStyle(element)
        const { width } = getComputedStyle(element)

        element.style.width = width
        element.style.position = 'absolute'
        element.style.visibility = 'hidden'
        element.style.height = ''

        const { height } = getComputedStyle(element)
        element.style.width = ''
        element.style.position = ''
        element.style.visibility = ''
        element.style.height = '0px'

        // Force repaint to make sure the
        // animation is triggered correctly.
        // eslint-disable-next-line no-unused-expressions
        getComputedStyle(element).height

        requestAnimationFrame(() => {
          // eslint-disable-next-line no-param-reassign
          element.style.height = height
        })
        console.log('enter3', element)
      },
      leave(element: Element) {
        console.log('leave', element)

        const { height } = getComputedStyle(element);
        (element as HTMLElement).style.height = height

        // Force repaint to make sure the
        // animation is triggered correctly.
        // eslint-disable-next-line no-unused-expressions
        getComputedStyle(element).height

        requestAnimationFrame(() => {
          (element as HTMLElement).style.height = '0px'
        })
      },
    }
  },
})

</script>

<style scoped>
* {
  will-change: height;
  transform: translateZ(0);
  backface-visibility: hidden;
  perspective: 1000px;
}
</style>

<style>

.expand-enter-active,
.expand-leave-active {
  transition: height 1s ease-in-out;
  overflow: hidden;
}

.expand-enter,
.expand-leave-to {
  height: 0;
}
</style>

<template>
  <Transition
    name="expand" :css="false"
    @enter="enter" @leave="leave"
  >
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
    const duration = 250
    return {
      show,
      enter(element: Element, done) {
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
        element.style.overflow = 'hidden'

        const keyframes = [
          { height: '0px', opacity: '0' },
          { height, opacity: '1' },
        ]
        const options = { duration, easing: 'ease-in-out' }

        const animation = element.animate(keyframes, options)
        animation.onfinish = () => {
          // Set height to 'auto' to keep UI adaptivity
          element.style.height = ''
          element.style.overflow = ''
          done()
        }
      },

      leave(element: Element, done) {
        const { height } = getComputedStyle(element)
        element.style.height = height
        element.style.overflow = 'hidden'
        console.log('leave', height)

        const keyframes = [
          { height, opacity: '1' },
          { height: '0px', opacity: '0' },
        ]
        const options = { duration, easing: 'ease-in-out' }

        const animation = element.animate(keyframes, options)
        animation.onfinish = () => {
          // Set height to 'auto' to keep UI adaptivity
          element.style.height = ''
          element.style.overflow = ''
          done()
        }
      },
    }
  },
})

</script>

<style scoped>
* {
  will-change: height;
}
</style>

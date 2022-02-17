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
        const options = { duration: 1250, easing: 'ease-in-out' }

        const animation = element.animate(keyframes, options)
        // We need to set a final height to 'auto' and we will do it right after
        // launching the animation, as soon as it will not go live before the
        // end of animation
        element.style.height = ''
        animation.onfinish = done()
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
}
</style>

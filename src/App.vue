<template>
  <div class="app-wrap">
    <header>
      <button
        v-for="(item, index) of tabs"
        :key="item"
        class="head-item"
        :class="{ on: index === activeIndex }"
        @click="tapItem(index)"
      >
        {{ item }}
      </button>
    </header>
    <main>
      <Component :is="currentComponent" />
    </main>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import ScrollTop from './ScrollTop.vue'
import GetBoundingClientRect from './GetBoundingClientRect.vue'
import IntersectionObserve from './IntersectionObserve.vue'

const tabs = ['scrollTop', 'getBoundingClientRect', 'intersectionObserve']
const activeIndex = ref(0)

const currentComponent = computed(() => {
  const comps = [ScrollTop, GetBoundingClientRect, IntersectionObserve]
  return comps[activeIndex.value]
})

const tapItem = (index) => {
  activeIndex.value = index
}
</script>

<style lang="scss" scoped>
.on {
  background-color: lightblue;
}
</style>

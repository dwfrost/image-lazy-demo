<template>
  <div ref="parentRef" class="Get-bounding-client-rect-wrap" @scroll="onScroll">
    <div ref="itemRef" v-for="(item, index) of imgs" :key="index" class="item">
      <img alt="" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { imgs } from './constant'

const parentRef = ref(null)
const itemRef = ref(null)

const onScroll = () => {
  const { top: parentTop, bottom: parentBottom } =
    parentRef.value.getBoundingClientRect()

  itemRef.value.forEach((item, index) => {
    const { top: childTop } = item.getBoundingClientRect()
    if (childTop < parentTop || childTop > parentBottom) return

    const { children } = item
    if (children?.[0] && !children[0].src) {
      children[0].src = imgs[index]
    }
  })
}
</script>

<style lang="scss" scoped>
.Get-bounding-client-rect-wrap {
  height: 600px;
  border: 1px solid;
  overflow: scroll;
  .item {
    min-height: 200px;
    img {
      display: block;
    }
  }
}
</style>

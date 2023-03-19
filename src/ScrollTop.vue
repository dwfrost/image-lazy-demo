<template>
  <div class="Scroll-top-wrap" @scroll="onScroll">
    <div ref="itemRef" v-for="(item, index) of imgs" :key="index" class="item">
      <img alt="" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { imgs } from './constant'

const itemRef = ref(null)

const onScroll = (e) => {
  const { scrollTop, clientHeight } = e.target

  itemRef.value.forEach((item, index) => {
    if (scrollTop + clientHeight <= item.offsetTop) return

    const { children } = item
    if (children?.[0] && !children[0].src) {
      children[0].src = imgs[index]
    }
  })
}
</script>

<style lang="scss" scoped>
.Scroll-top-wrap {
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

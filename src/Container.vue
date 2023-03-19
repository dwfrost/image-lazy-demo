<template>
  <div class="Scroll-top-wrap">
    <div v-for="(item, index) of imgs" :key="index" class="item">
      <img :src="item" alt="" />
    </div>
  </div>
</template>

<script setup>
import { imgs } from './constant'
</script>

<style lang="scss" scoped>
.Scroll-top-wrap {
  height: 600px;
  border: 1px solid;
  overflow: scroll;
}
</style>

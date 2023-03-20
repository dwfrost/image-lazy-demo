<template>
    <div class="Intersection-observe-wrap">
        <img ref="itemRef" v-for="(item, index) of imgs" :key="index" class="item" alt="" :data-src="item" />
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { imgs } from './constant'

const itemRef = ref(null)

onMounted(() => {
    const observerInstance = new IntersectionObserver(entries => {
        entries.forEach(item => {
            // console.dir(item.target)

            if (item.intersectionRatio > 0) {
                item.target.src = item.target.dataset.src
                observerInstance.unobserve(item.target)
            }
        })
    })

    itemRef.value.forEach(item => {
        observerInstance.observe(item)
    })
})
</script>

<style lang="scss" scoped>
.Intersection-observe-wrap {
    height: 600px;
    border: 1px solid;
    overflow: scroll;
    .item {
        min-height: 200px;
        display: block;
    }
}
</style>

<!--
 * @Author: Lqf
 * @Date: 2021-11-03 10:54:05
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2022-04-10 16:16:02
 * @Description: 我添加了修改
-->
<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  // value: Number,
  modelValue: Number,
  theme: { type: String, default: 'orange' },
})

// 修改主题颜色
const themeObj = {
  black: '#00',
  white: '#fff',
  red: '#f5222d',
  orange: '#fa541c',
  yellow: '#fadb14',
  green: '#73d13d',
  blue: '#40a9ff',
}
const fontStyle = computed(() => `color: ${themeObj[props.theme]}`)

// 评分宽度
const width = ref(props.value)
function mouseOver(i) {
  width.value = i
}
function mouseOut() {
  width.value = props.modelValue
}
width.value = props.modelValue
const fontWidth = computed(() => `width: ${width.value * 13.06}px`)

// 事件派发
const emits = defineEmits(['update:modelValue'])
// let emits = defineEmits('update-rate')
function onRate(num) {
  // emits('update-rate', num)
  emits('update:modelValue', num)
}

</script>

<template>
  <div :style="fontStyle">
    <slot />
    <div class="rate" @mouseout="mouseOut">
      <span v-for="num in 5" :key="num" class="solid" @mouseover="mouseOver(num)">☆</span>
      <span class="hollow" :style="fontWidth">
        <span v-for="num in 5" :key="num" @click="onRate(num)" @mouseover="mouseOver(num)">★</span>
      </span>
    </div>
  </div>
</template>

<style lang="less" scoped>
.rate {
  position: relative;
  display: inline-block;
  text-align: left;
}

.rate > span.solid {
  display: inline-block;
  width: 13.06px;
  text-align: center;
}
.rate > span.hollow {
  position: absolute;
  display: inline-block;
  top: 0;
  left: 0;
  width: 0;
  overflow: hidden;
}
</style>

<template>
  <section class="progress-bar-view">
    <el-button v-if="isShowButton" type="primary" @click="startCheck">开始检测</el-button>
    <section v-else class="progress-bar">
      <div id="bar" class="progress" :style="{ width: `${progress}%` }"></div>
    </section>
  </section>
</template>

<script setup lang="ts">
import { ref, nextTick, onMounted } from 'vue'
let isShowButton = ref(true)
let progress = ref(0)
let bar = ref()
onMounted(() => {
  bar.value = document.getElementById("bar")
})
const startCheck = () => {
  progress.value = 0;
  isShowButton.value = false;
  nextTick(() => {
    bar.value.style.width = 0 + "px";
  })
  startAnimation();
}
const startAnimation = () => {
  let intervalObj = setInterval(() => {
    if (progress.value >= 98) {
      clearInterval(intervalObj);
      progress.value = 100;
      isShowButton.value = true
    } else {
      progress.value++
    }
  }, 100);
}
</script>

<style lang="scss" scoped>
.progress-bar-view {
  width: 100%;
  height: 100%;

  .progress-bar {
    position: relative;
    overflow: hidden;
    width: 300px;
    height: 30px;
    background: rgba(20, 21, 23, 0.8);
    border-radius: 15px;
    border: 1px solid #0E0E0E;

    &::before {
      position: absolute;
      display: block;
      content: '检测中';
      width: 65px;
      height: 12px;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);

      font-size: 12px;
      line-height: 12px;
      font-weight: 400;
      color: #FFFFFF;
    }
  }

  .progress {
    height: 100%;
    // background-color: #009A39;
    background-image: linear-gradient(90deg, #009A39, #189099, #5aa9dd, #fff);
    border-radius: 15px;
    transition: width 0.01s ease-in-out;
    // border: 1px solid lightgray;
    // border: 1px solid #0E0E0E;
  }

}
</style>

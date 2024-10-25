<template>
  <div class="cn-char">
    <div class="title">
      笔画查询
    </div>
    <div class="content">
      <el-input v-model="words" size="large" style="width: 240px" placeholder="输入查询汉字"/>
    </div>
    <div class="option">
      <el-button @click="reDraw" type="primary" size="large" :icon="Search">查询</el-button>
      <el-button @click="clear" type="danger" size="large" :icon="Delete">清空</el-button>
    </div>
    <span v-show="show">动画</span><div id='drawAnimation' :key="key"/>
    <span v-show="show">笔画</span><div id='drawStroke' :key="key"/>
  </div>

</template>

<script lang="ts" setup>
import draw from 'cnchar-draw';
import {ref} from "vue";
import {
  Delete,
  Search,
} from '@element-plus/icons-vue'

draw.setResourceBase('https://char.zhhhs.dscloud.me:12000/draw/')

const words = ref('')

const show = ref(false)

const key = ref(1)

const clear = () => {
  key.value++
  words.value = ''
  show.value = false
}

const reDraw = () => {
  draw(words.value, {
    el: '#drawStroke',
    type: draw.TYPE.STROKE
  })
  draw(words.value, {
    el: '#drawAnimation',
    type: draw.TYPE.ANIMATION,
    animation:{
      loopAnimate: true
    }
  })
  show.value = true
}

</script>
<style scoped lang="css">

.title {
  text-align: center;
  color: rgba(36, 58, 168, 0.98);
  font-size: 30px;
  margin-bottom: 30px;
}

.option {
  margin-top: 10px;
  margin-bottom: 10px;
}
</style>


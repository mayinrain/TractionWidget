<template>
    <BTagSelector :clearable="true" v-model:selectedList="thirdVal" :options="[{ value: '我是太阳', label: '太阳' }, { value: '我是月亮', label: '月亮' },{ value: '我是地球', label: '地球' }, { value: '我是火星', label: '火星' },{ value: '我是M87星云', label: 'M87星云' }, { value: '我是木星', label: '木星' }, { value: '我是呀哈哈', label: '呀哈哈' }, { value: '我是金星', label: '金星' }]" label="计数" tagKey="value" @selectorChange="handleChange" @clearAll="handleClear">
         <template v-slot:header>
             <div class="title-text">选中tag计数: {{ thirdVal.length }}</div>
         </template>
    </BTagSelector>
</template>
<script setup lang="ts">
import { BTagSelector } from '@fesjs/traction-widget';

import { ref } from 'vue';
// 选择器所绑定的数据
const thirdVal = ref<string[]>([]);
// 数据变化的回调
const handleChange = (val: any) => {
    console.log(val);
};

const handleClear = ()=>{
    console.log('clear all')
}
</script>
<style scoped>
.title-text {
    font-family: PingFangSC-Medium;
    font-size: 14px;
    color: #0f1222;
    letter-spacing: 0;
    line-height: 32px;
    font-weight: 500;
}
</style>

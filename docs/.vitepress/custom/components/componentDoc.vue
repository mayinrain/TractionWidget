<template>
  <div class="component-doc">

    <span class="play" @click="openPlayground">Play</span>
    <div class="component-doc-content">
      <slot></slot>
    </div>
    <div :class="['component-doc-code', visibleCode && 'visible-code']" v-html="currentCode"></div>
    <div class="component-doc-header" @click="toggleCode">
      <!-- <LeftOutlined :class="['show-code-btn', visibleCode && 'active']" @click="toggleCode" /> -->
      {{visibleCode ? '收起代码' : '查看代码'}}
      <DownOutlined :class="['show-code-btn', visibleCode && 'active']" />
    </div>
  </div>

</template>
<script setup lang="ts">
import {
    watch,
    ref,
    computed
} from 'vue';
import { DownOutlined } from '@fesjs/fes-design/icon';
import { debounce } from 'lodash-es';
import playground from './playground';
import codes from './demoCode.json';

const props = defineProps({
  codeName: String,
  codeSrc: String,
  codeFormat: String,
});
const code = ref('');
const currentCode = computed(() =>
    decodeURIComponent(props?.codeFormat || ''),
);

const visibleCode = ref(false);
const openPlayground = debounce(() => {
  playground({
      codeName: props.codeName,
      codeSrc: props.codeSrc,
  });
}, 500);

const toggleCode = () => {
    visibleCode.value = !visibleCode.value;
};
</script>
<style lang="less" scoped>
.play {
  position: absolute;
  right: 16px;
  top: 12px;
  cursor: pointer;
  &:hover {
    color: #108981;
  }
}
.component-doc {
  margin-top: 16px;
  border: 1px solid #cfd0d3;
  border-radius: 4px;
  position: relative;
  .component-doc-content {
    padding-top: 48px;
  }
  &-header {
    height: 48px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    border-top: 1px solid #cfd0d3;
    font-size: 14px;
    padding: 0 16px;
    cursor: pointer;

    .show-code-btn {
      cursor: pointer;
      transition: 0.3s all;
      transform-origin: center center;

      &.active {
        transform: rotateZ(-180deg);
      }
    }
  }

  &-content {
    padding: 16px;
  }

  &-code {
    max-height: 720px;
    border-top: 1px solid #cfd0d3;
    transition: all 0.3s;
    opacity: 0;
    height: 0;
    font-size: 14px;
    overflow: auto;

    &.visible-code {
      border-radius: 4px;
      opacity: 1;
      height: auto;
      padding: 16px;
      background-color: #292d3e;
    }
  }
}
</style>

<template>
    <FDrawer v-model:show="isShow" title="Playground" displayDirective="show" width="90%" @ok="isShow = false"
    >
        <Repl
            v-if="props.codeName"
            :editor="CodeMirror"
            :store="store"
            :show-ts-config="false"
            :show-import-map="true"
            :show-compile-output="false"
            :clear-console="false"
        />
    </FDrawer>
</template>

<script setup>
import { ref, version, watch } from 'vue';

import CodeMirror from '@vue/repl/codemirror-editor';
import { Repl, ReplStore } from '@vue/repl';

import { FDrawer } from '@fesjs/fes-design';
import { DEMO_ENTRY_FILE, FES_DESIGN_SETUP } from './constants';

const props = defineProps({
    codeName: String,
    codeSrc: String,
});
const mainFile = 'src/App.vue';
const demoFile = 'src/demo.vue';

const store = new ReplStore({
    defaultVueRuntimeURL: `https://registry.npmmirror.com/vue/${version}/files/dist/vue.esm-browser.js`,
});

const defaultFiles = {
    [mainFile]: DEMO_ENTRY_FILE,
    'src/fes-design.js': FES_DESIGN_SETUP,
    'import-map.json': JSON.stringify({
        imports: {
            '@fesjs/fes-design':
                'https://registry.npmmirror.com/@fesjs/fes-design/latest/files/dist/fes-design.esm-browser.js',
            '@fesjs/fes-design/icon':
                'https://registry.npmmirror.com/@fesjs/fes-design/latest/files/dist/fes-design.icon-browser.js',
            // 切npm库
            '@fesjs/traction-widget':
                'https://cdn.jsdelivr.net/npm/@fesjs/traction-widget/dist/traction-widget.esm-browser.js',
            // 切本地库
            // '@fesjs/traction-widget':
            //     'http://127.0.0.1:8080/packages/traction-widget/dist/traction-widget.esm-browser.js'
        },
    }),
};
store.setFiles(defaultFiles);
store.setActive(mainFile);
function resolveSFCExample(codeSrc) {
    defaultFiles[demoFile] = codeSrc;
    return defaultFiles;
}

function updateExample(codeSrc) {
    store.setFiles(resolveSFCExample(codeSrc), mainFile).then(() => {
        store.setActive(demoFile);
    });
}

watch(
    () => props.codeSrc,
    () => {
        updateExample(decodeURIComponent(props.codeSrc));
    },
    {
        immediate: true,
    },
);

const isShow = ref(true);
function handleShow(val) {
    isShow.value = val;
}
defineExpose({
    isShow,
    handleShow,
});
</script>

<style lang="less">
.vue-repl {
    border-right: 1px solid var(--vt-c-divider-light);
    height: calc(100vh - 55px); // 55px 是 drawer header 的宽度
}

.fes-repl-drawer-content {
    .fes-drawer-body-container {
        padding-top: 0;
        padding-right: 0;
        padding-bottom: 0;
    }
}
</style>

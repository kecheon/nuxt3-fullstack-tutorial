<script setup lang="ts">
import Editor from '@toast-ui/editor';
import '@toast-ui/editor/dist/toastui-editor.css';
// const Editor = () => import('@toast-ui/editor');

const props = defineProps({
  modelValue: {
    type: String,
    required: false,
    default: 'test',
  },
});
const emit = defineEmits(['update:modelValue']);
const domEl = document.createElement("div");
const editor = ref<HTMLElement>(domEl);
onMounted(() => {
  const e = new Editor({
    el: editor.value,
    height: '500px',
    initialEditType: 'markdown',
    previewStyle: 'vertical',
    events: {
      change: () => emit('update:modelValue', e.getMarkdown()),
    },
  });
});
</script>

<template>
    <div ref="editor"></div>
</template>
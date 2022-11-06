<script setup lang="ts">
import Editor from '@toast-ui/editor';
import '@toast-ui/editor/dist/toastui-editor.css';
// const Editor = () => import('@toast-ui/editor');

const props = defineProps({
  modelValue: {
    type: String,
    required: false,
    default: '',
  },
});
const emit = defineEmits(['update:modelValue']);
const editor = ref<HTMLElement>();
onMounted(() => {
  const e = new Editor({
    el: editor.value,
    height: '500px',
    initialEditType: 'markdown',
    previewStyle: 'vertical',
    initialValue: props.modelValue,
    theme: 'dark',
    events: {
      change: () => emit('update:modelValue', e.getMarkdown()),
    },
  });
});
</script>

<template>
    <div ref="editor" />
</template>
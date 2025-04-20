<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';
import { MDCRipple } from '@material/ripple';

defineProps({
  /** 按钮类型 */
  type: {
    type: String as () => 'button' | 'submit' | 'reset',
    default: 'button'
  },
  /** 按钮名称 */
  name: {
    type: String,
    default: ''
  },
  /** 是否禁用 */
  disabled: {
    type: Boolean,
    default: false
  }
});

const element = ref<HTMLButtonElement | null>(null);
let button: MDCRipple | null = null;

onMounted(() => {
    if (element.value) {
        button = new MDCRipple(element.value);
    }
})

onBeforeUnmount(() => {
  if (button) {
    button.destroy();
  }
});
</script>q

<template>
    <button class="mdc-button mdc-button--raised" ref="element"
    :type="type" :name="name" :disabled="disabled">
      <span class="mdc-button__ripple"></span>
      <span class="mdc-button__label"><slot></slot></span>
    </button>
</template>

<style scoped lang="scss">
@use "@material/button/styles";
</style>

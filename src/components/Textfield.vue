<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';
import { MDCTextField } from '@material/textfield';

defineProps({
  /** 按钮类型 */
  type: {
    type: String as () => 'text' | 'password' | 'email',
    default: 'text'
  },
  /** 按钮名称 */
  name: {
    type: String,
    default: ''
  },
  /** 是否必需 */
  required: {
    type: Boolean,
    default: false
  },
  /** 错误提示 */
  helperline: {
    type: String,
    default: null
  }
});

const element = ref<HTMLLabelElement | null>(null);
let textfield: MDCTextField | null = null;

onMounted(() => {
    if (element.value) {
        textfield = new MDCTextField(element.value);
    }
})

onBeforeUnmount(() => {
  if (textfield) {
    textfield.destroy();
  }
});
</script>

<template>
    <label class="mdc-text-field mdc-text-field--outlined" ref="element">
      <span class="mdc-notched-outline">
        <span class="mdc-notched-outline__leading"></span>
        <span class="mdc-notched-outline__notch">
          <span class="mdc-floating-label"><slot></slot></span>
        </span>
        <span class="mdc-notched-outline__trailing"></span>
      </span>
      <input :type="type" :name="name" :required="required" class="mdc-text-field__input" aria-labelledby="label">
    </label>

    <div class="mdc-text-field-helper-line" v-if="helperline">
      <div class="mdc-text-field-helper-text mdc-text-field-helper-text--validation-msg" aria-hidden="true">{{ helperline }}</div>
    </div>
</template>

<style scoped lang="scss">
@use "@material/floating-label/mdc-floating-label";
@use "@material/line-ripple/mdc-line-ripple";
@use "@material/notched-outline/mdc-notched-outline";
@use "@material/textfield";

@include textfield.core-styles;
</style>

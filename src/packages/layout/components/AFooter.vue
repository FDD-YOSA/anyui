<template>
  <header class="a-layout-inner a-footer" :style="styles">
    <slot></slot>
  </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    // height of the footer, need to be a valid CSS height string
    height: {
      type: [Number, String],
      default: '',
    },
  },
  setup(props) {
    const height = typeof props.height === 'number' ? `${props.height}px` : props.height;
    const styles = {
      height: height || '',
    };
    return {
      styles,
    };
  },
});
</script>

<style lang="scss">
.a-footer {
  height: var(--a-footer-height);
  line-height: var(--a-footer-height);
  box-sizing: border-box;
}
</style>

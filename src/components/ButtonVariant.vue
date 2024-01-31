<template>
  <button
    :class="['btn', `btn-${variant}`]"
    :style="{ width: customWidth ? '100%' : `${customWidth}px` }"
    @click="onClick"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "ButtonVariant",
  props: {
    variant: {
      type: String,
      default: "primary",
    },
    variant: {
      type: String,
      default: "none",
    },
    customWidth: {
      type: [Number, String],
      default: "auto",
    },
  },
  methods: {
    onClick(event) {
      this.$emit("click", event);
    },
  },
};
</script>

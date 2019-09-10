<template>
  <button :class="['button', {'button--outlined': outlined}]" @click="handleClick">
    <slot />
  </button>
</template>
<script>
export default {
  name: "BaseButton",
  methods: {
    handleClick(event) {
      this.$emit("click", event);
    }
  },
  props: {
    outlined: {
      type: [Boolean, String],
      default: false
    }
  }
};
</script>
<style lang="scss">
.button {
  padding: 10px 20px;
  background: red;
  &--outlined {
    background: green;
  }
}
</style>
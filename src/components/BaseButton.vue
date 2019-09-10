<template>
  <button :class="['button', {'button--outshined': outshined}]" @click="handleClick">
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
    outshined: {
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
  &--outshined {
    background: aqua;
  }
}
</style>
<template>
  <h1 :class="['nice', {'nice--capital': capital}]">
    <slot />
  </h1>
</template>

<script>
export default {
  name: "HOne",
  props: {
    capital: {
      type: [Boolean, String],
      default: false
    }
  }
};
</script>

<style lang  = "scss">
.nice {
  color: salmon;
  &--capital {
    text-transform: uppercase;
    color: blueviolet;
  }
}
</style>
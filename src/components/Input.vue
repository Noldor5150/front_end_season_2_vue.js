<template>
  <div class="text-field">
    <label v-if="labelText" class="text-field__label" :for="`text_field${_uid}`">{{labelText}}</label>
    <input @input="handleInput" v-bind="$attrs" :id="`text_field${_uid}`" class="text-field__input" />
    <small v-if="helperText" class="text-field__helper">{{helperText}}</small>
  </div>
</template>
<script>
export default {
  name: "BaseTextField",
  inheritAttrs: false,
  data() {
    return {
      defaults: { type: "text" }
    };
  },
  computed: {
    attrs() {
      const defaults = { type: "text" };
      return { ...defaults, ...this.$attrs };
    }
  },
  methods: {
    handleInput(event) {
      this.$emit("input", event);
    }
  },
  props: {
    labelText: {
      type: String,
      default: null
    },
    helperText: {
      type: String,
      default: null
    }
  }
};
</script>
<style lang='scss'>
.text-field {
}
</style>
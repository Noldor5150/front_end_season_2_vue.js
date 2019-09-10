<template>
  <div class="app">
    <BaseButton @click="handleClick">ALIO</BaseButton>

    <HOne v-if="!isVisible">Sheize</HOne>
    <HOne v-else :capital="true">Hilo</HOne>
    <Input label-text="Email" type="email" placeholder="test" @input="onInput" />
  </div>
</template>

<script>
export default {
  name: "App",
  components: {
    BaseButton,
    HOne,
    Input
  },
  data() {
    return { isVisible: false };
  },
  methods: {
    handleClick(event) {
      this.isVisible = !this.isVisible;
    },
    onInput(event) {
      console.log(event);
    }
  }
};
import BaseButton from "@/components/BaseButton";
import HOne from "@/components/HOne";
import Input from "@/components/Input";
</script>


<style>
</style>
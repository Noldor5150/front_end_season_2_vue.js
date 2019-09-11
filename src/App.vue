<template>
  <div class="app">
    <BaseButton :outshined="aquaButton" @click="handleClick">ALIO</BaseButton>

    <HOne v-if="!isVisible">Sheize</HOne>
    <HOne v-else :capital="true">Hilo</HOne>
    <Input v-model="email" label-text="Email" type="email" placeholder="test" />
    {{email}}
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
    return { isVisible: false, email: null, aquaButton: false };
  },
  methods: {
    handleClick(event) {
      this.isVisible = !this.isVisible;
      this.aquaButton = !this.aquaButton;
    }
  }
};
import BaseButton from "@/components/BaseButton";
import HOne from "@/components/HOne";
import Input from "@/components/Input";
</script>


<style>
</style>
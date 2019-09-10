<template>
  <div class="app">
    <BaseButton @click="handleClick">show</BaseButton>
    <BaseButton :outlined="true" @click="handleClick">hide</BaseButton>
    <p
      v-if="isVisible"
    >Lorem ipsum dolor sit amet consectetur adipisicing elit. Deleniti consectetur architecto rem quo! Distinctio, atque rerum, adipisci a error impedit cupiditate iusto dignissimos, voluptatibus amet nisi! Fuga, fugit nam. Reprehenderit.</p>
    <HOne v-if="!isVisible">Sheize</HOne>
    <HOne v-else :capital="true">Hilo</HOne>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {
    BaseButton,
    HOne
  },
  data() {
    return { isVisible: false };
  },
  methods: {
    handleClick(event) {
      this.isVisible = !this.isVisible;
    }
  }
};
import BaseButton from "@/components/BaseButton";
import HOne from "@/components/HOne";
</script>


<style>
</style>
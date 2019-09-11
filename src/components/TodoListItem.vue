<template>
  <li :class="['todo-list-item', {'todo-list-item--checked':todo.isDone}]">
    <input type="checkbox" :checked="todo.done" @change="handleChange" />
    {{todo.text}}{{todo.isDone}}
    <button @click="handleDelete">Delete</button>
  </li>
</template>

<script>
export default {
  name: "TodoListItem",
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods: {
    handleChange(event) {
      this.$emit("change", event);
    },
    handleDelete(event) {
      this.$emit("delete", event);
    }
  }
};
</script>

<style lang="scss">
.todo-list-item {
  text-transform: uppercase;
  color: blueviolet;
  &--checked {
    text-decoration: line-through;
  }
}
</style>
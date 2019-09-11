<template>
  <div class="app">
    <HOne v-if="!isVisible">Sheize</HOne>
    <HOne v-else :capital="true">Hilo</HOne>
    <Input v-model="newTodoText" label-text="test" type="text" placeholder="test" />
    <!-- {{email}} -->
    <BaseButton :outshined="aquaButton" @click="handleClick">ALIO</BaseButton>
    <div class="alio">
      <TodoList>
        <TodoListItem
          v-for="(todo, index) in todos"
          :key="index"
          :todo="todo"
          @change="handleChange(index, $event)"
          @delete="handleDelete(index, $event)"
        ></TodoListItem>
      </TodoList>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {
    BaseButton,
    HOne,
    Input,
    TodoList,
    TodoListItem
  },
  data() {
    return {
      isVisible: false,
      email: null,
      aquaButton: false,
      newTodoText: null,
      todos: [],
      checked: false
    };
  },
  methods: {
    handleClick(event) {
      this.isVisible = !this.isVisible;
      this.aquaButton = !this.aquaButton;
      const todo = { text: this.newTodoText, isDone: false };
      if (todo.text) {
        this.todos.push(todo);
        this.newTodoText = null;
      }
    },
    handleChange(index, event) {
      this.todo = this.todos.map((todo, todoIndex) => {
        if (index === todoIndex) {
          todo.isDone = event.target.checked;
        }
        return todo;
      });
    },
    handleDelete(index, event) {
      this.todos = this.todos.filter((todo, todoIndex) => {
        if (index !== todoIndex) {
          return true;
        }
      });
    }
  }
};
import BaseButton from "@/components/BaseButton";
import HOne from "@/components/HOne";
import Input from "@/components/Input";
import TodoList from "./components/TodoList";
import TodoListItem from "./components/TodoListItem";
</script>


<style lang ="scss">
</style>
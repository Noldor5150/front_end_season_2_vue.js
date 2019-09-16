<template>
  <div class="app">
    <div class="surface">
      <h1 class="headline">
        <i class="material-icons">assignment_turned_in</i>
        Todo List
        <BaseButton
          v-for="filter in filters"
          :key="filter"
          :oulined="filter !==activeFilter"
          class="surface__filter"
          @click="addFilter(filter)"
        >{{filter}}</BaseButton>
        <BaseButton
          v-for="type in sortedTypes"
          :key="type"
          :oulined="type !==sortedBy"
          class="surface__filter"
          @click="setSortedBy(type)"
        >{{type}}</BaseButton>
      </h1>
      <h4 class="headline headline--4">{{ today }}</h4>

      <div class="surface__new">
        <BaseTextField
          v-model="newTodoText"
          placeholder="What needs to be done?"
          class="surface__input"
          @keydown.enter="addNewTodo"
        />
        <BaseButton class="surface__button" @click="addNewTodo">
          <i class="material-icons">playlist_add</i>
        </BaseButton>
      </div>

      <div v-if="todos.length > 0" class="surface__todos">
        <TodoList>
          <TodoListItem
            v-for="todo in filteredTodos"
            :key="todo.id"
            :todo="todo"
            @change="handleChange(todo.id, $event)"
            @updated="updateTodoItem"
            @delete="handleDelete(todo.id)"
          />
        </TodoList>
      </div>
    </div>
  </div>
</template>

<script>
import uniqid from "uniqid";
import BaseButton from "@/components/BaseButton";
import BaseTextField from "@/components/BaseTextField";
import TodoList from "@/components/TodoList";
import TodoListItem from "@/components/TodoListItem";

const LS_TODOS = "todos";

export default {
  name: "App",
  components: {
    BaseButton,
    BaseTextField,
    TodoList,
    TodoListItem
  },
  data() {
    return {
      activeFilter: "all",
      sortedBy: "asc",
      sortedTypes: ["asc", "desc"],
      filters: ["all", "completed", "inprogress"],
      newTodoText: null,
      todos: JSON.parse(localStorage.getItem("LS_TODOS")) || []
    };
  },
  computed: {
    filteredTodos() {
      const filteredTodos = this.todos.filter(todo => {
        switch (this.activeFilter) {
          case "all":
            return true;
          case "completed":
            return todo.done;
          case "inprogress":
            return !todo.done;
          default:
            return true;
        }
      });
      if (this.sortedBy === "asc") {
        return filteredTodos.sort((a, b) => a.time - b.time);
      }
      if (this.sortedBy === "desc") {
        return filteredTodos.sort((a, b) => b.time - a.time);
      }
      return filteredTodos;
    },

    today() {
      return new Date().toLocaleString("en-GB", {
        weekday: "long",
        month: "long",
        day: "2-digit"
      });
    }
  },
  watch: {
    todos() {
      this.updateLS();
    }
  },

  methods: {
    updateLS() {
      localStorage.setItem("LS_TODOS", JSON.stringify(this.todos));
    },
    addFilter(value) {
      this.activeFilter = value;
    },
    setSortedBy(type) {
      this.sortedBy = type;
    },
    addNewTodo(event) {
      if (!this.newTodoText) return;
      const todo = {
        id: uniqid(),
        time: Date.now(),
        text: this.newTodoText,
        done: false
      };
      this.todos = [...this.todos, todo];
      this.newTodoText = null;
    },

    handleChange(id, event) {
      this.todos = this.todos.map(todo => {
        if (todo.id === id) {
          todo.done = event.target.checked;
        }
        return todo;
      });
    },

    handleDelete(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    updateTodoItem(newTodo) {
      this.todos = this.todos.map(todo => {
        if (todo.id === newTodo.id) {
          return newTodo;
        }
        return todo;
      });
    }
  }
};
</script>

<style lang="scss">
.app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100%;
  padding: 1.5rem;
}

.headline {
  display: flex;
  align-items: center;
  font-size: 1.75rem;
  margin: 0;
  margin-bottom: 1.5rem;

  &--4 {
    font-size: 1.15rem;
    font-weight: normal;
    color: rgba(black, 0.51);
  }

  .material-icons {
    font-size: 2.5rem;
    margin-right: 0.5rem;
  }
}

.surface {
  background-color: white;
  padding: 2rem;
  border-radius: 4px;
  box-shadow: 0px 1px 3px 0px rgba(0, 0, 0, 0.1);
  max-width: 600px;
  width: 100%;

  &__new {
    display: flex;
    margin-bottom: 1.5rem;
  }

  &__input {
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
    border-right: 0;
  }

  &__button {
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
  }
}
</style>

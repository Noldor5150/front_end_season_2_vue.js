<template>
  <li :class="['todo-list-item', {
      'todo-list-item--done': todo.done
    }]">
    <input
      :id="todo.id"
      :value="todo.id"
      :disabled="inEdit"
      :checked="todo.done"
      type="checkbox"
      @change="handleChange"
    />

    <label v-if="!inEdit" :for="todo.id" class="todo-list-item__text">{{ todo.text }}</label>
    <input v-else v-model="updatedText" type="text" />
    <span class="todo-list-item__time">{{ createdAt }}</span>
    <button class="todo-list-item__button" @click="handleEdit">
      <i class="material-icons">edit</i>
    </button>
    <button class="todo-list-item__button" @click="handleDelete">
      <i class="material-icons">delete</i>
    </button>
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
  data() {
    return {
      updatedText: this.todo.text,
      inEdit: false
    };
  },
  computed: {
    createdAt() {
      return new Date(this.todo.time).toLocaleTimeString("en-GB", {
        timeStyle: "short",
        hour12: true
      });
    }
  },
  methods: {
    handleChange(event) {
      If(!this.inEdit);
      return this.$emit("change", event);
    },

    handleDelete(event) {
      this.$emit("delete", event);
    },
    handleEdit() {
      this.inEdit = !this.inEdit;
      if (this.updatedText !== this.todo.text) {
        this.$emit("updated", { ...this.todo, text: this.updatedText });
      }
    }
  }
};
</script>

<style lang="scss">
.todo-list-item {
  display: flex;
  align-items: center;
  background-color: whitesmoke;
  padding: 0 1rem;
  margin-bottom: 1rem;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  border-bottom: 1px solid #ccc;

  &--done {
    .todo-list-item__text {
      text-decoration: line-through;
      color: rgba(black, 0.31);
    }
  }

  &__text {
    flex: 1;
    font-weight: bold;
    font-size: 0.975rem;
    margin-left: 1rem;
    padding: 1rem 0;
    padding-right: 1rem;

    &:hover {
      cursor: pointer;
    }
  }

  &__time {
    margin-right: 1rem;
    color: rgba(black, 0.51);
    user-select: none;
    text-transform: uppercase;
    font-size: 0.875rem;
  }

  &__button {
    -webkit-appearance: none;
    background-color: transparent;
    border: 0;
    padding: 0;

    &:focus {
      outline: 0;
      opacity: 0.75;
    }

    &:hover {
      cursor: pointer;
      opacity: 0.75;
    }
  }
}
</style>

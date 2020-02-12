<template>
  <div class="todos">
    <h2 class="title">Todos</h2>
    <AddTodo v-on:add-todo="addTodo" />
    <TodosFilter v-if="todos.length !== 0" v-on:show-all="showAll" v-on:show-completed="showCompleted" />
    <p class="no-todos" v-if="todos.length === 0">No todos.</p>
    <ul class="todos__list" v-if="todos.length !== 0">
      <li class="todos__list-item" v-for="todo in todos" v-bind:key="todo.id">
        <TodoItem v-bind:todo="todo" v-on:delete-todo="deleteTodo" />
      </li>
    </ul>
  </div>
</template>
<script>
import uuid from "uuid";
import TodoItem from "./todoItem";
import AddTodo from "../addTodo";
import TodosFilter from "../todosFilter";

export default {
  name: "TodoList",
  components: {
    TodoItem,
    AddTodo,
    TodosFilter
  },
  data() {
    return {
      todos: [],
      allTodos: []
    };
  },
  methods: {
    addTodo(todo) {
      this.todos.push({
        id: uuid.v4(),
        text: todo,
        isCompleted: false
      });
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    showAll() {
      this.todos = this.allTodos;
    },
    showCompleted() {
      this.allTodos = this.todos;
      this.todos = this.todos.filter(todo => todo.isCompleted);
    }
  }
};
</script>

<style lang="scss" scoped>
.todos {
  padding-top: 60px;

  .title {
    margin-bottom: 16px;
  }

  .no-todos {
    text-align: left;
  }

  &__list {
    list-style-type: none;
  }
  &__list-item {
    text-align: left;
    &:last-child {
      .item {
        margin-bottom: 0;
      }
    }
  }
}
</style>
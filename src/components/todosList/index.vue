<template>
  <div class="todos">
    <h2 class="title">Todos List</h2>
    <AddTodo v-on:add-todo="addTodo" />
    <TodosFilter
      v-on:show-all="showAll"
      v-on:show-completed="showCompleted"
      v-on:show-active="showActive"
      :count="remainingTodosCount"
    />
    <p class="no-todos" v-if="todos.length === 0">No todos.</p>
    <ul class="todos__list" v-if="todos.length !== 0">
      <li class="todos__list-item" v-for="todo in todos" v-bind:key="todo.id">
        <TodoItem
          :todo="todo"
          v-on:delete-todo="deleteTodo"
          v-on:toggle-is-completed="toggleIsCompleted"
        />
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
      todos: []
    };
  },
  mounted: function() {
    this.todos = this.getTodosFromStorage();
  },
  computed: {
    remainingTodosCount: function() {
      const todos = this.getTodosFromStorage();
      return todos.filter(todo => !todo.isCompleted).length;
    }
  },
  methods: {
    getTodosFromStorage: function() {
      const todos = localStorage.getItem("todos") || "[]";
      const parsedTodos = JSON.parse(todos);
      return parsedTodos;
    },
    saveTodosToStorage: function(todos) {
      localStorage.setItem("todos", JSON.stringify(todos));
    },
    addTodo(todo) {
      this.todos.push({
        id: uuid.v4(),
        text: todo,
        isCompleted: false
      });
      this.saveTodosToStorage(this.todos);
    },
    showAll() {
      this.todos = this.getTodosFromStorage();
    },
    showCompleted() {
      const todos = this.getTodosFromStorage();
      this.todos = todos.filter(todo => todo.isCompleted);
    },
    showActive() {
      const todos = this.getTodosFromStorage();
      this.todos = todos.filter(todo => !todo.isCompleted);
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
      this.saveTodosToStorage(this.todos);
    },
    toggleIsCompleted: function(id) {
      this.todos = this.todos.map(todo => {
        if (todo.id === id) {
          return {
            ...todo,
            isCompleted: !todo.isCompleted
          };
        }
        return todo;
      });
      this.saveTodosToStorage(this.todos);
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
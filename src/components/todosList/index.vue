<template>
  <div class="todos">
    <h2 class="title">Todos List</h2>
    <AddTodo v-on:add-todo="addTodo" />
    <TodosFilter
      v-on:show-all="showAll"
      v-on:show-completed="showCompleted"
      v-on:show-active="showActive"
      :count="remainingTodosCount()"
    />
    <p class="no-todos" v-if="todos.length === 0">No todos.</p>
    <Dragable
      v-model="todos"
      tag="ul"
      class="todos__list"
      v-bind="dragOptions"
      @start="startDrag"
      @end="endDrag"
      v-if="todos.length !== 0"
    >
      <transition-group type="transition" :name="!drag ? 'flip-list' : null">
        <li class="todos__list-item list-group-item" v-for="todo in todos" :key="todo.id">
          <TodoItem
            :todo="todo"
            v-on:delete-todo="deleteTodo"
            v-on:toggle-is-completed="toggleIsCompleted"
          />
        </li>
      </transition-group>
    </Dragable>
  </div>
</template>
<script>
import uuid from "uuid";
import TodoItem from "./todoItem";
import AddTodo from "../addTodo";
import TodosFilter from "../todosFilter";
import Dragable from "vuedraggable";

export default {
  name: "TodoList",
  components: {
    TodoItem,
    AddTodo,
    TodosFilter,
    Dragable
  },
  display: "Transitions",
  data() {
    return {
      todos: [],
      drag: false,
      dragOptions: {
        animation: 200,
        group: "description",
        disabled: false,
        ghostClass: "ghost"
      }
    };
  },
  mounted: function() {
    this.todos = this.getTodosFromStorage();
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
    },
    remainingTodosCount: function() {
      const todos = this.getTodosFromStorage();
      return todos.filter(todo => !todo.isCompleted).length;
    },
    startDrag: function() {
      this.drag = false;
    },
    endDrag: function() {
      this.drag = false;
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
.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
.list-group-item {
  cursor: move;
}
</style>
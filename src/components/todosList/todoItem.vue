<template>
  <div class="item">
    <div class="item__actions">
      <i class="fa fa-trash" @click="deleteTodo"></i>
      <input type="checkbox" name="check" @click="toggleIsCompleted" :checked="todo.isCompleted" />
    </div>
    <p v-bind:class="{ 'is-completed': todo.isCompleted }" class="text">{{todo.text}}</p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    toggleIsCompleted() {
      this.$emit("toggle-is-completed", this.todo.id);
    },
    deleteTodo() {
      this.$emit("delete-todo", this.todo.id);
    }
  }
};
</script>
<style lang="scss" scoped>
.item {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  margin-bottom: 16px;
  padding: 18px;
  background-color: #fff;
  border-radius: 4px;
  box-shadow: 0px 0px 16px #e2e2e2;

  .text {
    font-size: 16px;
    color: #0a0a0a;
    line-height: 1.5;
    &.is-completed {
      text-decoration: line-through;
      color: #979797;
    }
  }
  &__actions {
    display: flex;
    justify-content: flex-start;
    margin-right: 8px;
    i {
      padding-left: 6px;
      cursor: pointer;
      font-size: 12px;
      &.fa-trash {
        color: #d0021b;
      }
    }
    input[type="checkbox"] {
      width: 14px;
      height: 14px;
      margin-left: 6px;
      cursor: pointer;
    }
  }
}
</style>
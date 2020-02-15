<template>
  <div class="item">
    <div class="item__actions">
      <img class="trash" src="https://img.icons8.com/android/24/000000/trash.png" />
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
    align-items: center;
    margin-right: 16px;
    .trash {
      cursor: pointer;
      width: 16px;
    }
    input[type="checkbox"] {
      width: 14px;
      height: 14px;
      margin-left: 8px;
      cursor: pointer;
    }
  }
}
</style>
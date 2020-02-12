<template>
  <div class="filter-actions">
    <button @click="showAll" class="action-btn">Show All</button>
    <button @click="showCompleted" class="action-btn">Completed</button>
  </div>
</template>
<script>
export default {
  name: "TodosFilter",
  methods: {
    showAll() {
      this.$emit("show-all");
    },
    showCompleted() {
      this.$emit("show-completed");
    }
  }
};
</script>
<style lang="scss" scoped>
.filter-actions {
  text-align: left;
  margin-bottom: 16px;

  .action-btn {
    border: 0;
    height: 28px;
    padding: 0 8px;
    background-color: #22988d;
    color: #fff;
    border-radius: 4px;
    font-size: 14px;
    cursor: pointer;
    margin-right: 8px;
    &:last-child {
      margin-right: 0;
    }
  }
}
</style>
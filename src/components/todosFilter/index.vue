<template>
  <div class="filter-section">
    <div class="cont">
      <p @click="showActive">{{count}} {{count | pluralized}} left</p>
    </div>
    <div class="filter-actions">
      <button @click="showAll" class="action-btn">Show All</button>
      <button @click="showActive" class="action-btn">Active</button>
      <button @click="showCompleted" class="action-btn">Completed</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "TodosFilter",
  props: ["count"],
  methods: {
    showAll() {
      this.$emit("show-all");
    },
    showCompleted() {
      this.$emit("show-completed");
    },
    showActive() {
      this.$emit("show-active");
    }
  },
  filters: {
    pluralized: function(count) {
      return count === 1 ? "todo" : "todos";
    }
  }
};
</script>
<style lang="scss" scoped>
.filter-section {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 8px;
}
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
.cont {
  p {
    cursor: pointer;
  }
}
</style>
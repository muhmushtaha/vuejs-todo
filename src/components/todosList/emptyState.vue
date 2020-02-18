<template>
  <div class="empty-state">
    <p>No {{tabName}} Todos.</p>
    <i v-if="tabName == ''" class="hint">Click here to add a todo</i>
    <button v-if="tabName == ''" @click="foucsOnInput" class="add-btn">Add</button>
  </div>
</template>

<script>
export default {
  name: "EmptyState",
  props: ["activeTab"],
  methods: {
    foucsOnInput: function() {
      const inputElm = document.getElementById("todo-input");
      inputElm.focus();
    }
  },
  computed: {
    tabName: function() {
      switch (this.activeTab) {
        case "all":
          return "";
        case "active":
          return "active";
        case "completed":
          return "completed";
        default:
          return "";
      }
    }
  }
};
</script>
<style lang="scss" scoped>
.empty-state {
  height: 200px;
  width: 100%;
  border: 2px dashed #979797;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
p {
  margin-bottom: 8px;
}
.hint {
  font-size: 14px;
}
.add-btn {
  border: 0;
  height: 28px;
  padding: 0 8px;
  background-color: #22988d;
  color: #fff;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  margin-top: 8px;
}
</style>
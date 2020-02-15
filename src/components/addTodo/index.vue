<template>
  <form @submit="handleSubmit" class="form">
    <div class="form-group">
      <input
        autofocus
        class="input"
        type="text"
        name="todo"
        id="todo"
        v-model="text"
        placeholder="Learn VueJS"
      />
      <button :disabled="text.trim().length === 0" class="submit-btn" type="submit">Submit</button>
    </div>
  </form>
</template>
<script>
export default {
  name: "AddTodo",
  data() {
    return {
      text: ""
    };
  },
  methods: {
    handleTextChange(e) {
      this.text = e.target.value;
    },
    handleSubmit(e) {
      e.preventDefault();
      if (!this.text.trim().length) {
        return;
      }
      this.$emit("add-todo", this.text);
      this.text = "";
    }
  }
};
</script>
<style lang="scss" scoped>
.form {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 32px;
  .form-group {
    label {
      padding-right: 8px;
      font-size: 18px;
      line-height: 32px;
    }
    .input {
      height: 32px;
      border-radius: 4px 0 0 4px;
      border: 0;
      padding: 0 8px;
      min-width: 300px;
      border: 1px solid #e2e2e2;
      border-right: 0;
    }
    .submit-btn {
      border: 0;
      height: 34px;
      padding: 0 16px;
      background-color: #22988d;
      color: #fff;
      border-radius: 0 4px 4px 0;
      font-size: 16px;
      cursor: pointer;
      &:disabled {
        cursor: not-allowed;
      }
    }
  }
}
@media only screen and (max-width: 420px) {
  .form {
    // flex-direction: column;
    .form-group {
      .input {
        max-width: 100%;
        min-width: 100%;
      }
    }
  }
}
</style>
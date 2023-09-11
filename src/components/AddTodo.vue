<template>
  <form @submit.prevent="addTodo" class="form">
    <input
      type="text"
      v-model="title"
      placeholder="Add a todo..."
      class="search"
    />
    <input type="submit" value="Add" class="btn" />
  </form>
</template>
<script>
export default {
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTodo(e) {
      const newTodo = {
        title: this.title,
        completed: false,
      };
      this.$emit("add-todo", newTodo);
      this.title = "";
    },
  },
};
</script>

<style scoped>
.form {
  display: flex;
  margin: 30px;
  height: 36px;
  flex-wrap: wrap;
}
.search {
  flex: 75%;
  margin-right: 46px;
}
.btn {
  flex: 15%;
  background-color: beige;
}
</style>

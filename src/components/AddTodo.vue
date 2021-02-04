<template>
  <div id="add-todo">
    <form @submit.prevent="handleSubmit">
      <input
        type="text"
        v-model="todo.description"
        placeholder="what's on your mind"
      />
      <button>Add todo</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "add-todo",
  data() {
    return {
      todo: {
        description: "",
        completed: false,
      },
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("add:todo", this.todo);
      //
      // this.todo.description = ""
    },
  },
};
</script>

<style>
#add-todo {
  width: 750px;
  margin-top: -10px;
  padding: 5px;
}
</style>

<template>
  <div id="todo-list">
    <table>
      <thead>
        <tr>
          <th>todo</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todo in todos" :key="todo.id">
          <!-- if editing === id means click edit and is editing  -->
          <td v-if="editing === todo.id">
            <input type="text" v-model="todo.description" />
          </td>
          <td v-else-if="completedTodo == true"></td>
          <td v-else>{{ todo.description }}</td>
          <!-- cannot call function delete() with this.todo -->

          <td v-if="editing === todo.id">
            <i
              @click="editTodo(todo)"
              class="fa fa-check"
              aria-hidden="true"
            ></i>
            <i
              @click="cancelEdit(todo)"
              class="fa fa-times"
              aria-hidden="true"
            ></i>
          </td>
          <td v-else-if="completedTodo == true">
            completed task actions
          </td>
          <td v-else>
            <i
              id="edit-button"
              @click="editMode(todo)"
              class="fa fa-pencil fa-1x"
            ></i>
            <i
              id="trash-button"
              @click="$emit('delete:todo', todo.id)"
              class="fa fa-trash-o fa-1x"
            ></i>
          </td>
        </tr>

        <tr v-if="completedTodo === null">
          <button @click="completedMode">Completed</button>
        </tr>
        <tr v v-else>
          <button @click="activeMode">Active</button>
          <button>Clear All</button>
        </tr>
      </tbody>
    </table>
    <h1>hello world</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      editing: null,
      cachedTodo: null,
      completedTodo: null,
    };
  },
  name: "todo-list",
  props: {
    todos: Array,
  },
  methods: {
    editMode(todo) {
      this.cachedTodo = Object.assign({}, todo);
      this.editing = todo.id;
    },
    editTodo(todo) {
      if (todo.description === "") return;
      this.$emit("edit:todo", todo.id, todo);
      this.editing = null;
    },
    cancelEdit(todo) {
      Object.assign(todo, this.cachedTodo);
      this.editing = null;
    },
    completedMode() {
      this.completedTodo = true;
    },
    activeMode() {
      this.completedTodo = null;
    },
  },
  computed: {},
};
</script>

<style>
#todo-list {
  /* margin: -25px 0px 0px 0px; */
  /* padding: 20px; */
  width: 75%;
  font-size: 15px;
}
button {
  /* blank space between buttons */
  margin-top: 5px;
  margin-right: 10px;
  width: auto;
  font-size: 12px;
  padding: 5px;
}

i {
  margin: 0px 10px 0px 0px;
}

#edit-button {
  color: dodgerblue;
}
#trash-button {
  color: crimson;
}
</style>

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


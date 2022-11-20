<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <h3>You have {{ todosCount }} Todos!</h3>
    <div>
      <input
        v-model="newTodoName"
        @keyup.enter="addTodo()"
        type="text"
        placeholder="Add a Todo"
      />
    </div>
    <div>
      <ul>
        <li v-for="todo in todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="deleteTodo(todo.id)">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodoName: "",
      todos: [
        { id: 1, name: "One" },
        { id: 2, name: "Two" },
        { id: 3, name: "Three" },
      ],
      exclamations: ["Bingo", "Damn", "Bravo"],
    };
  },
  computed: {
    todosCount() {
      return this.todos.length;
    },
  },
  methods: {
    addTodo() {
      let newTodo = {
        id: Date.now(),
        name: this.newTodoName,
      };
      this.todos.push(newTodo);
      this.newTodoName = ""; //clear the input field
    },
    deleteTodo(id) {
      this.todos.splice(id, 1);
    },
  },
  watch: {
    newTodoName(newValue) {
      console.log("newValue:", newValue);
      if (this.exclamations.includes(newValue.toLowerCase())) {
        this.newTodoName = "";
        alert("You must NEVER say ", newValue, " !!");
      }
    },
  },
};
</script>
<style>
ul {
  list-style: none;
  padding: 0;
  width: 200px;
  margin: 20px auto 0;
}
li {
  border: 1px solid;
  display: flex;
  margin-bottom: 10px;
}
li span {
  flex-grow: 1;
}
</style>
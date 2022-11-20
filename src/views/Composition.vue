<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <h3>You have {{ todosCount }} Todos!</h3>
    <div>
      <input
        v-model="data.newTodoName"
        @keyup.enter="addTodo()"
        type="text"
        placeholder="Add a Todo"
      />
    </div>
    <div>
      <ul>
        <li v-for="todo in data.todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="deleteTodo(todo.id)">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { computed, watch, reactive } from "vue";
export default {
  setup() {
    const exclamations = ["Bingo", "Damn", "Bravo"]; //not reactive variables

    let data = reactive({
      newTodoName: "",
      todos: [
        { id: 1, name: "One" },
        { id: 2, name: "Two" },
        { id: 3, name: "Three" },
      ],
    });
    let todosCount = computed(() => {
      return data.todos.length;
    });

    function addTodo() {
      let newTodo = {
        id: Date.now(),
        name: data.newTodoName,
      };
      data.todos.push(newTodo);
      data.newTodoName = ""; //clear the input field
    }
    function deleteTodo(id) {
      data.todos.splice(id - 1, 1);
    }

    watch(data, (newValue) => {
      if (exclamations.includes(newValue.newTodoName.toLocaleLowerCase())) {
        alert("You must NEVER say", newValue.newTodoName, " !!");
        data.newTodoName = "";
      }
    });
    return {
      data,
      addTodo,
      deleteTodo,
      todosCount,
    };
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
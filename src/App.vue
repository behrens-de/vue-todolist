<template>
  <div class="bg-gray-100 text-dark max-w-2xl rounded-md mx-5 md:mx-auto my-5">
    <h1 class="py-2 text-2xl text-center">Meine Todoliste</h1>
    <h2 class="pb-2 text-1xl text-gray-500 text-center">
      Noch offen: {{ todos.filter((todo) => !todo.done).length }}
    </h2>
    <div class="w-full bg-gray-200 flex justify-center p-1">
      <input type="text" class="grow w-full px-3 mr-1" v-model="newTodo" />
      <button @click="addTodo" class="bg-green-600 text-white py-1 px-3">
        Anlegen
      </button>
    </div>

    <!-- Scheifen in VUE -->
    <div v-for="(todo, index) in todos" :key="index">
      <Todo
        :todoProps="todo"
        :todoIndex="index"
        @toggel-done="toggleDone"
        @remove-todo="removeTodo"
      />
    </div>

    <!-- Binding
    <Todo :todoProps="todos[0].label" />
    <Todo :todoProps="todos[1].label" />
    <Todo :todoProps="todos[2].label" />

    Übergabe ohne Binding
    <Todo todoProps="NOT BINDED PROP" /> -->
  </div>
</template>

<script>
import Todo from "./components/Todo.vue";
export default {
  name: "App",
  components: {
    Todo,
  },
  data() {
    return {
      newTodo: "",
      todos: [
        {
          label: "Was machen",
          done: false,
        },
        {
          label: "Etwas lachen",
          done: true,
        },
        {
          label: "Lass krachen",
          done: false,
        },
      ],
    };
  },
  methods: {
    addTodo() {
      if(this.newTodo.trim() === '') return;
      this.todos.push({
        label: this.newTodo,
        done: false,
      });

      this.newTodo = "";
    },
    toggleDone(index) {
      this.todos[index].done = !this.todos[index].done;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<!--/CSS-->
<style scoped>
* {
  color: #3e3e3e;
}

input {
  outline: none;
}
</style>

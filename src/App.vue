<template>
  <div
    class="bg-gray-100 text-dark max-w-2xl rounded-md mx-5 md:mx-auto my-5 shadow-lg border-1 border border-gray-200"
  >
    <h1 class="py-2 text-2xl text-center">{{ headline }}</h1>

    <!-- Alternative oder unsauber ? 
    <h2 class="pb-2 text-1xl text-gray-500 text-center">
      {{ openTodos > 0 ? "Noch Offen " + openTodos : "Keine Todos offen" }}
    </h2>
    -->

    <h2 class="pb-2 text-1xl text-gray-500 text-center">
      <div v-if="todos.length < 1">Lege eine Todo an!</div>
      <div v-else>
        <div v-if="openTodos > 0">Noch offen {{ openTodos }}</div>
        <div v-else-if="todos">Keine offenen Todos!</div>
      </div>
    </h2>

    <div class="w-full bg-gray-200 flex justify-center p-1">
      <input
        type="text"
        placeholder="Aufgabe anlegen..."
        class="grow w-full px-3 mr-1"
        v-model="newTodo"
      />
      <button @click="addTodo" class="bg-green-600 text-white py-1 px-3">
        {{ buttonText }}
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
      headline: "Meine Todoliste",
      buttonText: "Hinzufügen",
      newTodo: "",
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() === "") return;

      this.todos.push({
        label: this.newTodo,
        done: false,
      });

      this.newTodo = "";
      this.storeTodos();
    },
    toggleDone(index) {
      this.todos[index].done = !this.todos[index].done;
      this.storeTodos();
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
      this.storeTodos();
      // console.log(index);
      // console.log(this.todos[index]);
    },
    storeTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
  mounted() {
    // VUE - MOUNTED LIFE CICLE
    let data = localStorage.getItem("todos");
    if (data !== "" && data !== null && data !== undefined) {
      this.todos = JSON.parse(data);
    }
  },
  computed: {
    openTodos() {
      return this.todos.filter((t) => !t.done).length;
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

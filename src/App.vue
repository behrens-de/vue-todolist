<template>
  <div class="bg-gray-100 text-dark max-w-2xl rounded-md mx-5 md:mx-auto my-5">
    <h1 class="py-2 text-2xl text-center">Meine Todoliste</h1>
    <h2 class="pb-2 text-1xl text-gray-500 text-center">
      Noch offen: {{ todos.length }}
    </h2>
    <div class="w-full bg-gray-200 flex justify-center p-1">
      <input type="text" class="grow w-full px-3 mr-1" />
      <button @click="demo" class="bg-green-600 text-white py-1 px-3">
        Anlegen
      </button>
    </div>
    <Todo message="Hallo" />
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
      todos: [
        {
          label: "Was machen",
          done: 0,
        },
        {
          label: "Etwas lachen",
          done: 0,
        },
        {
          label: "Lass krachen",
          done: 0,
        },
      ],
    };
  },
  methods: {
    demo() {
      alert(this.input);
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

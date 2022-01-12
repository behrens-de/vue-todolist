<template>
  <div
    class="flex justify-between items-center bg-white p-2 border border-indigo-200 m-2"
    :class="{ 'bg-green-600': todo.done, 'bg-red-600': !todo.done }"
  >
    <h1 @click="toggleTodo" class="cursor-pointer">{{ todo.label }}</h1>
    <button
      @click="removeTodo"
      class="bg-indigo-500 text-xs text-white py-1 px-3 rounded-sm"
    >
      Löschen
    </button>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: ["todoProps", "todoIndex"],
  data() {
    return {
      todo: this.todoProps,
    };
  },
  methods: {
    toggleTodo() {
      // EMIT SCHICKZ EINEN BESTIMMTEN WERT AN DIE ÜBERGEORDNETE KOMPONENTE
      this.$emit("toggel-done", this.todoIndex);
    },
    removeTodo() {
      // EMIT SCHICKZ EINEN BESTIMMTEN WERT AN DIE ÜBERGEORDNETE KOMPONENTE
      this.$emit("remove-todo", this.todoIndex);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

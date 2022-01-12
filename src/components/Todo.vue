<template>
  <h1>{{message.toUpperCase()}}</h1>
  <span>{{count}}</span>
  <button v-on:click="countUp">Hochzählen</button>
  <button @click="countDown">Runterzählen</button>
</template>

<script>
export default {
  name: 'Todo',
  data(){
    return {
      message: "ich bin eine Message!",
      count: 0
    }
  },
  methods:{
    countUp(){
      this.count++
    },
    countDown(){
      this.count--
    }
  }
}
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

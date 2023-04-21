<script>
import CreateTask from './components/CreateTask.vue'

export default {
  name: 'App',
  components: {
    CreateTask,
  },
  data() {
    return {
      items: [],
    }
  },
  methods: {
    addItem(item) {
      this.items.push(item)
      console.log(this.items);
    },

  }
}
</script>

<template>
  <header>
    <h1 class="appTitle">Todo App</h1>,
    <CreateTask :items="items" @add-item="addItem" />
    <ul><li v-for="item in items" style="color: blue">{{ item }}</li></ul>
  </header>

</template>

<style scoped>

header {
  line-height: 1.5;
  width: 60vw;
  min-height: 60vh;
  
}

@media (min-width: 512px) {
  header {
    display: flex;
    flex-direction: column;
    background-color: #fff;
    place-items: top;
    border-radius: 5px;
  }

  .appTitle {
  margin-left: 10%;
  padding-top: 2rem;
  display: block;
  color: black;
}
}
</style>

   



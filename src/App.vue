<script>
import CreateTask from './components/CreateTask.vue'
import Task from './components/Task.vue'

export default {
  name: 'App',
  components: {
    CreateTask,
    Task,
  props: ['task']
  },
  data() {
    return {
      items: [],
      task:"",
    }
  },
  methods: {
    addItem(item) {
      this.items.push(item)
      console.log(this.items);
    },

    deleteItem(index) {
      this.items.splice(index, 1)
    },

    editItem(index) {
      this.task = this.items[index],
      console.log(this.task);
    }
  }
}
</script>

<template>
  <header>
    <h1 class="appTitle">Todo App</h1>,
    <CreateTask :items="items" @add-item="addItem" :value="this.task"/>

    <ul>
      <Task v-for="(item, index) in items" :key="index" @delete="deleteItem(index)"
      @edit="editItem(index)">{{ item }}</Task>
    </ul>
  </header>

</template>

<style scoped>

header {
  line-height: 1.5;
  width: 60vw;
  min-height: 60vh;
}

ul li {
  list-style-type: none;
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

   



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

  mounted() {
    
    if(localStorage.getItem('items')) {
      try {
        this.items = JSON.parse(localStorage.getItem('items'));
      } catch(e) {
        localStorage.removeItem('items');
      }
    }
  },

  methods: {
    addItem(item) {
      this.items.push({name:item, editing:false, completed:false})
      console.log(this.items);
      this.saveItems();
    },

    deleteItem(index) {
      this.items.splice(index, 1);
      this.saveItems();
    },

    editItem(index) {
      this.task = this.items[index],
      console.log(this.task);
    },

    clearAllItems() {
      this.items = [];
      this.saveItems();
    },
    
    clearCompleted() {
      this.items = this.items.filter(completed);
      this.saveItems();
    },

    completedItems(index) {
      this.items[index].completed = !this.items[index].completed;
    },

    saveItems() {
      let parsed = JSON.stringify(this.items);
      localStorage.setItem('items', parsed);
    }
  }
}
</script>

<template>
  <header>
    <h1 class="appTitle">Todo App</h1>,
    <CreateTask :items="items" @add-item="addItem" :value="this.task"/>

    <ul>
      <Task v-for="(item, index) in items" 
      :key="index"
      :class= "{ completed: item.completed}"
      @delete="deleteItem(index)"
      @edit="editItem(index)"
      @click="completedItems(index)"
      >{{ item.name }}</Task>
    </ul>
    <div class="clearButtons">
      <button class="clearBtn" @click="clearAllItems"
      >Clear Completed</button>
      <button class="clearAllBtn" @click="clearAllItems">Clear All</button>
    </div>

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

.clearButtons {
  margin-left: 10%;
}

.completed {
  text-decoration: line-through
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

   



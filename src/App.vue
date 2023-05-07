<script>
import CreateTask from './components/CreateTask.vue'
import Task from './components/Task.vue'

export default {
  name: 'App',
  components: {
    CreateTask,
    Task
  },
  data() {
    return {
      items: [],
      editItem: null,
      lastID: 0
    }
  },

  mounted() {
    if (localStorage.getItem('items')) {
      try {
        this.items = JSON.parse(localStorage.getItem('items'))
      } catch (e) {
        localStorage.removeItem('items')
      }
    }
  },

  methods: {
    addItem(item) {
      this.items.push({ id: ++this.lastID, name: item, editing: false, completed: false })
      console.log(this.items)
      this.saveItems()
    },

    deleteItem(index) {
      this.items.splice(index, 1)
      this.saveItems()
    },

    editTask(id) {
      this.editItem = this.items.find((e) => e.id === id)
    },

    saveTask(name) {
      this.items.forEach((e, index) => {
        if (e.id === this.editItem.id) {
          this.items[index].name = name
        }
      })
      this.editItem = null
    },

    clearAllItems() {
      this.items = []
      this.saveItems()
    },

    clearCompleted() {
      this.items = this.items.filter((item) => !item.completed)
      this.saveItems()
    },

    completedItems(index) {
      this.items[index].completed = !this.items[index].completed
      this.saveItems()
    },

    saveItems() {
      let parsed = JSON.stringify(this.items)
      localStorage.setItem('items', parsed)
    }
  }
}
</script>

<template>
  <header>
    <h1 class="appTitle">Todo App</h1>
    ,
    <CreateTask :item="editItem" @add-item="addItem" @save-item="saveTask" />

    <ul>
      <Task
        v-for="(item, index) in items"
        :key="index"
        :class="{ completed: item.completed }"
        @delete="deleteItem(index)"
        @edit="editTask(item.id)"
        @click="completedItems(index)"
        >{{ item.name }}</Task
      >
    </ul>
    <p v-if="this.items.length === 0">For now you have nothing to do.</p>
    <div class="clearButtons">
      <button class="clearBtn" @click="clearCompleted">Clear Completed</button>
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

p {
  color: black;
  margin-left: 10%;
}

.clearButtons {
  margin-left: 10%;
}

.completed {
  text-decoration: line-through;
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

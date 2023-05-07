<script>
import App from '../App.vue'

export default {
  data() {
    return {}
  },

  methods: {
    deleteItem(index) {
      this.$emit('delete', index)
    },

    editItem(index) {
      this.$emit('edit', index)
    }
  }
}
</script>

<template>
  <li>
    <slot></slot>
    <div>
      <button @click="deleteItem(index)">delete</button>
      <button @click="editItem(index)">edit</button>
    </div>
  </li>
</template>

<style scoped>
li {
  color: black;
  margin-left: 10%;
  display: flex;
}
</style>

<script>
import App from '../App.vue'

export default {
  props: {
    item: {
      type: Object,
      default: null
    }
  },
  data() {
    return {
      name: ''
    }
  },

  watch: {
    item: {
      handler(newValue) {
        this.name = newValue?.name || ''
      },
      deep: true
    }
  },

  methods: {
    addItem() {
      this.$emit('add-item', this.name)
      this.name = ''
    },

    saveItem() {
      this.$emit('save-item', this.name)
    }
  }
}
</script>

<template>
  <div class="addComponent">
    <input class="newTask" v-model="name" />
    <button v-if="!item?.id" class="addBtn" type="submit" @click="addItem">Add</button>
    <button v-else class="editBtn" type="submit" @click="saveItem">Save</button>
  </div>
</template>

<style>
.addComponent {
  display: block;
}

.newTask {
  box-sizing: border-box;
  margin-left: 10%;
}

.addBtn {
  display: inline-block;
}
</style>

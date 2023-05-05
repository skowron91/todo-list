<script >
import App from '../App.vue';

export default {
  props: {
    items: ['items']
  },
data() {
  return {
    task: "",
  }
},

methods: {
  addItem() {
    this.$emit('add-item', this.task);
    this.task = "";
  },
  
}
}
</script>

<template>
  <div class="addComponent">
    <input class="newTask" 
      v-model="task" >
    <button class="addBtn" type="submit" @click="addItem">Add</button>
    
  </div>
  
</template>

<style>

.addComponent{
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
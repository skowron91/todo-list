<script >
import App from '../App.vue';

export default {
  
data() {
  return {
    insertedValue: '',
  }
},

methods: {
  addItem() {
    this.$emit('add-item', this.insertedValue);
    this.insertedValue = "";
  }
}
}
</script>

<template>
  <div class="addComponent">
    <input class="newTask" v-model="insertedValue">
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
<template>
 <div>
    <div class="container mt-5 p-5">
      <header-component msg="Page Title"/>
      <div class="form-group">
        <input type="text" v-model="newTask" class="form-control my-3" @keyup.enter="saveNewTask">
        <button class="btn btn-primary my-3" @click="saveNewTask">
          Add New Task
        </button>
      </div>
      <card-component @message="editTask" v-for="alert in todoList" :key="alert" :title="alert"/>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CardComponent from './components/Card.vue';
import HeaderComponent from './components/Header.vue';

export default defineComponent({
  name: 'App',
  data() {
    return {
      todoList: ['Ir a correr', 'Comprar en el almacen'],
      newTask: '',
      editing: false,
      index: -1,
    };
  },
  components: {
    CardComponent,
    HeaderComponent,
  },
  methods: {
    saveNewTask():void {
      const checkCondition = (this.index === -1 && !this.exists() && !this.editing && this.newTask !== '');
      if (checkCondition) {
        this.todoList.push(this.newTask);
      } else {
        this.todoList[this.index] = this.newTask;
        this.editing = false;
        this.index = -1;
      }
      this.clearNewTask();
    },
    clearNewTask():void {
      this.newTask = '';
    },
    newTaskIsEmpty():boolean {
      return this.newTask !== '';
    },
    editTask(title: string):void {
      this.index = this.todoList.indexOf(title);
      this.editing = true;
      this.newTask = title;
    },
    exists():boolean {
      return this.todoList.includes(this.newTask);
    },
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  background-color: whitesmoke;
}
</style>

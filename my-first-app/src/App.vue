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
      <card
        v-for="alert in todoList"
        :key="alert"
        :title="alert"
        @message="editTask"
        @title="deleteTask"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Card from './components/Card.vue';
import HeaderComponent from './components/Header.vue';

export default defineComponent({
  name: 'App',
  data() {
    return {
      todoList: ['Ir a correr', 'Comprar en el almacen'],
      newTask: '',
      isEditing: false,
      index: -1,
      EDITING_TASK: true,
      EDITED_TASK: false,
    };
  },
  components: {
    Card,
    HeaderComponent,
  },
  methods: {
    saveNewTask():void {
      const checkCondition = (this.index === -1 && !this.exists() && !this.isEditing && this.newTask !== '');

      if (checkCondition) {
        this.todoList.push(this.newTask);
      } else {
        this.modify(this.index, this.newTask);
        this.clearNewTask();
      }
    },
    clearNewTask():void {
      this.newTask = '';
    },
    newTaskIsEmpty():boolean {
      return this.newTask !== '';
    },
    editTask(title: string):void {
      this.index = this.getTaskIndex(title);
      this.setState(this.EDITING_TASK);
      this.newTask = title;
    },
    deleteTask(title: string): void {
      this.todoList = this.todoList.filter((task) => task !== title);
    },
    exists():boolean {
      return this.todoList.includes(this.newTask);
    },
    getTaskIndex(title: string):number {
      return this.todoList.indexOf(title);
    },
    setIndes(newIndex: number): void {
      this.index = newIndex;
    },
    setState(taskState: boolean): void {
      this.isEditing = taskState;
    },
    modify(index: number, task: string): void {
      this.todoList[index] = `${task} `;
      this.todoList[index].trim();
      this.setState(this.EDITED_TASK);
      this.index = -1;
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

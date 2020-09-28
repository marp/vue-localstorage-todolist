<template>
  <img alt="Vue logo" width="100" src="./assets/logo.png">
  <h1>Vue LocalStorage ToDo List</h1>
  <div id="newTask">
      <input v-model="newTaskInput" placeholder="What you have to do?">
      <button @click="addTask">Add Task</button>
  </div>
  <div id="tasksList">
  <div v-for="(task, index) in tasks" :key="index">
    <Task :task="task" :index="index" @remove="removeTask(index)" @done="doneTask(index)"/>
  </div>
  </div>
</template>

<script>
import Task from "@/components/Task";

export default {
  name: 'App',
  components: {
    Task
  },
  data() {
    return {
      tasks: [],
      newTaskInput: ''
    }
  },
  mounted() {
    if (localStorage.getItem('tasks')) {
      this.loadTasks();
    } else {
      this.tasks = [
          {content: 'Zakupy', done: false},
          {content: 'Spacer z psem', done: true},
          {content: 'Programowanie', done: false}
        ]
      this.saveTasks();
    }
  },
  watch: {

  },
  methods: {
    addTask(){
      // JSON.parse(localStorage.tasks).tasks.unshift({content: 'xd'});
      this.tasks.unshift({content: this.newTaskInput, done: false});
      this.newTaskInput = '';
      this.saveTasks();
    },
    removeTask(index){
      this.tasks.splice(index, 1);
      this.saveTasks();
    },
    doneTask(index){
      this.tasks[index].done = !(this.tasks[index].done);
      this.saveTasks();
    },
    saveTasks(){
      localStorage.tasks = JSON.stringify(this.tasks);
    },
    loadTasks(){
      this.tasks = JSON.parse(localStorage.tasks);
    }

  }

}
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #fcfcfc;
  width: 500px;
  margin-left: auto;
  margin-right: auto;
}

#newTask > input {
  width: 400px;
  padding: 10px;
}

button {
  height: 40px;
}

#tasksList{
  margin-left: 2px;
  width: 494px;
  text-align: left;
  border: #2c3e50 solid 1px;
}
</style>

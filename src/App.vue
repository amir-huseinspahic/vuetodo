<script setup>
import { ref, provide } from 'vue'

import TaskInput from './components/TaskInputComponent.vue'
import TaskList from './components/TaskList/TaskListComponent.vue'
import LinksFooter from './components/Links.vue'

let id = 0;
let tasks = ref([
  { "id": id++, text: "This is a task" },
]);

provide('tasksArray', tasks);

const addTask = (taskText) => {
  if (taskText.trim().length !== 0) {
    tasks.value.push({ id: id++, text: taskText });
  }
}

const removeTask = (taskID) => {
  tasks.value = tasks.value.filter((task) => task.id !== taskID)
}

const editTask = (taskID, newText) => {
  tasks.value.forEach((element) => {
    if (element.id === taskID) element.text = newText
  });
}
</script>

<template>
  <div class="wrapper">
    <div id="app-header"><h1 class="app-header-text">TODO Vue</h1></div>

    <TaskInput @create-new-task="addTask" />
    <TaskList :tasks="tasks" @remove-task="removeTask" @edit-task="editTask"/>
  </div>
  <LinksFooter />
</template>

<style>
.wrapper {
  background-color: #384152;
  padding: 3px;
  margin: 7px;
  border-radius: 10px;
}

#app-header {
  display: flex;
  justify-content: center;
}

.app-header-text {
  font-size: 3rem;
  background: -webkit-linear-gradient(45deg, rgba(55,204,67,1), rgba(74,130,224,1));
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
}

@media only screen and (min-width: 600px) {
  .wrapper {
    padding: 8px;
  }
}

@media only screen and (min-width: 1000px) {
  .wrapper {
    margin: 3rem auto 0px auto;
    width: 95%;
    max-width: 1200px;
    padding: 10px;
  }

  .app-header-text {
    font-size: 4rem;
    padding: 1rem 4px;
  }
}
</style>
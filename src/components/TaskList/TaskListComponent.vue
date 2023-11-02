<script setup>
import { inject } from 'vue'

import TaskComponent from './TaskComponent.vue'

import draggable from "vuedraggable";

const props = defineProps({
    tasks: Array
});

const tasksArray = inject('tasksArray')

const emit = defineEmits(['remove-task', 'edit-task', 'resort-array'])

function triggerRemovalEvent(taskID) {
    emit('remove-task', taskID);
}

function triggerEditEvent(taskID, newText) {
    emit('edit-task', taskID, newText);
}
</script>

<template>
    <div class="container">
        <h1 class="task-list-header">Tasks</h1>
        <draggable v-model="tasksArray" class="task-list" itemKey="newArray.id" tag="ul" :animation="300">
            <template #item="{ element: task }">
                <TaskComponent :task="task" @remove-task="triggerRemovalEvent" @edit-task="triggerEditEvent"/>
            </template>
        </draggable>
    </div>
</template>

<style scoped>

.container {
    display: block;
}

.task-list-header {
    text-align: center;
    margin-top: 28px;
    color: #838383;
    font-size: 2rem;
}

.task-list {
    list-style-type: none;
    padding: 2px;
}

@media only screen and (min-width: 1000px) {
    .task-list-header {
        text-align: unset;
    }
}
</style>
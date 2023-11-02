<script setup>
import { ref } from 'vue';

const props = defineProps({
    task: Object
});

const emit = defineEmits(['remove-task', 'edit-task']);

let editActive = ref(false);
let newText = ref("");

function toggleEdit() { editActive.value = !editActive.value; }

function triggerRemovalEvent(taskID) {
    emit('remove-task', taskID);
}

function triggerEditEvent(taskID, newText) {
    if (newText.trim().length === 0) newText = props.task.text
    emit('edit-task', taskID, newText);
    toggleEdit();
}

</script>

<template>
    <form @submit.prevent>
        <div class="container">
            <p class="task-text" v-if="!editActive">{{ task.text }}</p>
            <input class="edit-input" v-else :value="task.text" @input="newText = $event.target.value" type="text" autofocus>
            <div class="task-buttons">
                <template v-if="!editActive">
                    <button class="button-edit" @click="toggleEdit">EDIT</button>
                    <button class="button-delete" @click="triggerRemovalEvent(task.id)">DELETE</button>
                </template>
                <template v-else>
                    <button class="button-edit" @click="triggerEditEvent(task.id, newText)">DONE</button>
                    <button class="button-delete" @click="toggleEdit">CANCEL</button>
                </template>
            </div>
        </div>
    </form>
</template>

<style scoped>

.container {
    background-color: #111727;
    border-radius: 8px;
    margin: 5px 0px;
    padding: 6px;
    color: white;
    font-size: 18px;
}

.task-text {
    display: flex;
    align-items: center;
    background-color: #111727;
    border: none;
    padding: 2px;
}

.edit-input {
    background-color: #111727;
    border: none;
    color: white;
    width: 100%;
    font-style: italic;
    outline: none;
    font-size: 16px;
    transition: border-bottom 0.3s ease-in-out;
    border-bottom: 1px solid #111727;
}

.edit-input:focus {
    border-bottom: 1px solid white;
}

.task-buttons {
    margin-top: 10px;
}

.button-edit {
    background: -webkit-linear-gradient(45deg, rgba(55,204,67,1), rgba(74,130,224,1));
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    font-weight: bold;
    cursor: pointer;
    border: none;
    font-size: 1rem;
    transition: scale 0.2s ease-in;
}

.button-delete {
    color: red;
    background-color: #111727;
    font-weight: bold;
    cursor: pointer;
    border: none;
    margin-left: 10px;
    font-size: 1rem;
    transition: scale 0.2s ease-in;
}

@media only screen and (min-width: 600px) {
    .container {
        display: flex;
    }

    .task-buttons {
        margin: unset;
        margin-left: auto;
        display: flex;
        padding: 5px;
    }

    .button-delete {
        margin-left: 12px;
    }

    .button-edit:hover{
        scale: 1.1;
    }

    .button-delete:hover{
        scale: 1.1;
    }
}
</style>
<script setup>
import { ref } from 'vue';

    const emit = defineEmits (["create-new-task"]);

    const Greetings = ref({
        0: "What do you have in mind?",
        1: "Keeping busy?",
        2: "Let's get productive!",
        3: "Planning is half the work"
    });

    function getRandomGreeting() {
        return Greetings.value[Math.floor(Math.random() * 4)]
    }

    let taskText = ref("");
    let randomGreeting = getRandomGreeting();

    function triggerTaskInputEvent() {
        emit('create-new-task', taskText.value);
        taskText.value = "";
        randomGreeting = getRandomGreeting();
    }
</script>

<template>
    <form @submit.prevent>
        <div class="container">    
            <input class="task-input" v-model="taskText" id="taskInputID" type="text" :placeholder="randomGreeting">
            <button class="task-submit" @click="triggerTaskInputEvent">Add Task</button>
        </div>
    </form>
</template>

<style scoped>

.container {
    display: block;
}

.task-input {
    width: 100%;
    padding: 6px;
    font-size: 17px;
    background-color: #202838;
    color: white;
    border: none;
    border-radius: 7px;
    outline: solid 1px #202838;
    transition: outline 0.3s ease-in-out;
}

.task-submit {
    display: flex;
    justify-content: center;
    margin: 4px 8px;
    border: none;
    background: -webkit-linear-gradient(45deg, rgba(55,204,67,1), rgba(74,130,224,1));
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    font-weight: bold;
    font-size: 17px;
    cursor: pointer;
    transition: scale 0.2s ease-in;
}

@media only screen and (min-width: 600px) {
    .container {
        display: flex;
    }

    .task-input {
        width: 100%;
    }

    .task-input:focus {
        outline: solid 1px white;
    }

    .task-submit {
        display: flex;
        margin: unset;
        margin-left: auto;
        justify-content: center;
        align-items: center;
        padding: 6px;
        white-space: nowrap;
    }

    .task-submit:hover {
        scale: 1.1;
    }
}

@media only screen and (min-width: 1000px) {
    .task-input {
        border-radius: 12px;
        font-size: 18px;
        padding: 8px;
    }

    .task-submit {
        font-size: 20px;
        padding: 8px;
    }
}
</style>
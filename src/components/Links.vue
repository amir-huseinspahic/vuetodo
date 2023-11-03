<template>
<div class="container">
    <a href="https://github.com/amir-huseinspahic/vuetodo" target="_blank" rel="noopener noreferrer">
        Source
    </a>
    <a href="https://github.com/amir-huseinspahic" target="_blank" rel="noopener noreferrer">
        Github
    </a>
</div>
</template>

<style scoped>
.container {
    position: fixed;
    bottom: 0;
    display: flex;
    padding: 6px;
    background-color: #384152;
    width: 100%;
    justify-content: center;
    align-items: center;
}

.container a {
    color: lightgray;
    margin: 0px 12px;
    text-decoration: none;
    display: flex;
    margin: 0px 12px;
}

@media only screen and (min-width: 600px) {
    .container {
        padding: 10px;
    }

    .container a {
        margin: 0px 18px;
    }
}

</style>
<script setup lang="ts">
    import{
        ref,
    }from 'vue';

    interface Task {
    id: number;
    text: string;
    completed: boolean;
    favorite: boolean;
    }

    const newTask = ref("");
    const tasks = ref<Task[]>([]);

    function addTask(){
        const taskTitle = newTask.value.trim();

        if(!taskTitle) return;
        
        tasks.value.push({
            id: Date.now(),
            text: taskTitle,
            completed: false,
            favorite: false,
        });

        newTask.value = ""

        
    }

    function removeTask(id : number){
        tasks.value = tasks.value.filter((t) => t.id !== id);
    }
</script>

<template>
    <div class="wrapper">
        <h1>Todo App</h1>

        <div class="input-row">
            <input type="text" placeholder="Add Your Task's here..." v-model="newTask">
            <button @click="addTask">Add</button>
        </div>

        <ul class="task-list">
            <li v-for="task in tasks" :key="task.id" :class="{done: task.completed}">
                <button class="delete" @click="removeTask(task.id)">X</button>
                <input type="checkbox" class="is-done" v-model="task.completed">
                <span class="span">{{ task.text }}</span>
            </li>
        </ul>
    </div>
</template>

<style>

    body{
        margin: 0;
        background: linear-gradient(135deg, #6a11cb, #2575fc);
        min-height: 86vh;
        font-family: Arial, Helvetica, sans-serif;   
    }

    .wrapper{
        max-width: 500px;
        margin: 100px auto 0;
        background: #fff;
        text-align: center;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 20px 40px rgba(0,0,0,.25);
    }

    .input-row{
        padding: 12px 16px;
        font-size: 16px;   
        border-radius: 10px;
        outline: none;
        transition: all 0.3s ease;
        box-sizing: border-box;
    }

    .input-row button {
        padding: 12px 20px;
        margin-left: 10px;
        border: none;
        border-radius: 10px;
        background-color: #4f46e5;
        color: white;
        font-size: 16px;
        cursor: pointer;
        transition: background-color 0.3s;
    }

    .input-row button:hover {
        background-color: #4338ca;
    }

    .input-row input {
        width: 300px;
        padding: 14px 18px;
        border: 1px solid #2575fc;
        border-radius: 15px;
        background: rgba(255,255,255,0.1);
        backdrop-filter: blur(10px);
        font-size: 16px;
        outline: none;
    }

    .input-row input:focus{
        box-shadow: 20px 20px 28px rgba(79, 70, 229, 0.3);
    }

    .input-row input::placeholder {
        color: #888;
    }

    /* ul And li */

    li{
        position: relative;
        max-width: 378px;
        border-radius: 10px;
        list-style: none;
        text-align: left;
        background-color: #e4e4e4;
        padding: 20px;
        margin-bottom: 20px;
    }

    .span{
        position: relative;
        right: 25px;
    }

    .is-done{
        position: relative;
        right: 25px;
    }

    .task-list li.done span{
        text-decoration: line-through;
        opacity: .6;
    }

    /* delete task */

    .delete{
        position: relative;
        left: 350px;
        background-color: red;
        color: white;
        border: 1px solid black;
        height: 25px;
        width: 25px;
        border-radius: 6px;
    }
</style>
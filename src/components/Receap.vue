<script setup>
    import { ref,reactive } from 'vue';

    const users = reactive([]);
    const inpurSearch = ref("");
    const getUsers = ()=>{
        fetch('https://jsonplaceholder.typicode.com/users')
        .then((response) => response.json())
        .then((data) => {
            data.forEach(user => {
                users.push(user)
            })
        })
    }

    const todos = reactive([]);
    function getTodos(){
        fetch('https://jsonplaceholder.typicode.com/todos')
        .then((response) => response.json())
        .then((data)=>{
            data.forEach(todo=>{
                todos.push(todo)
            })
        })
    }
    getUsers();
    // getTodos();
    const filterUser=()=>{
        if(inpurSearch.value){
            return users.filter((user)=>{
                if(user.name.toLowerCase().includes(inpurSearch.value.toLowerCase()) || user.email.toLowerCase().includes(inpurSearch.value.toLowerCase())){
                    return user;
                }
            })
        }
        else{
            return users;
            }

    }
    const clearData =() =>{
        inpurSearch.value = "";
    }
</script>
<template>
    <ul>
        <input type="text" v-model="inpurSearch"> <button @click="clearData()">clear</button>
        <li v-for="(user,index) in filterUser()" :key="index"><strong>Name:</strong> {{ user.name }}--- Email:{{ user.email }}--- Username:{{ user.username }}</li>
        <li v-for="(todo,index) in todos" :key="index"><strong>Title :</strong> {{ todo.title }}</li>
    </ul>
</template>
<style scoped></style>
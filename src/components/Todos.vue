<template>
  <AddTodo @add-todo="addTodo" />
  <TodoItem class="todos" v-for="todo in todos" :key="todo.id" :todoProps="todo"
            @item-completed="markCompleted" @delete-item="deleteTodo"
  />

</template>

<script>

import {ref} from "vue";
import TodoItem from "@/components/TodoItem";
import AddTodo from "@/components/AddTodo";
// import {v4 as uuidv4} from 'uuid'
import axios from 'axios'

export default {
  name: "Todos",

  components:{TodoItem,AddTodo},
  setup() {
    const todos = ref([])
    const getAllTodos = async () => {
      try {
        const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
        todos.value = res.data
        console.log(res.data)
      } catch (error) {
        console.log(error)
      }
    }
    getAllTodos()
    const markCompleted = id => {
      todos.value = todos.value.map(todo => {
        if (todo.id === id ) todo.completed = !todo.completed;
        return todo
      })

    }
    const deleteTodo = async id => {
      try {
        await axios.delete('https://jsonplaceholder.typicode.com/todos/${id}')
        todos.value = todos.value.filter(todo => todo.id !== id)
      } catch (error) {
          console.log(error)
      }

    }
    const addTodo = async newItem => {
      try {
          const res = await axios.post('https://jsonplaceholder.typicode.com/todos',newItem)
          todos.value.push(res.data)


      } catch (error) {
        console.log(error)
      }

      // console.log(newItem.id)
      // todos.value.push(newItem)
    }


    return{
      todos,
      markCompleted,
      deleteTodo,
      addTodo,
    }
  }
}
</script>

<style scoped>

</style>

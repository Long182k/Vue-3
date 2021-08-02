<template>

  <p :class="['todo-items',todoProps.completed ? 'is-completed' : ' ' ]">
    <input type="checkbox" :checked="todoProps.completed" @change="markItemCompleted" />
    {{todoProps.title}}
    <button class="del-btn" @click="deleteItem"   > Delete </button>
  </p>
</template>

<script>
// import {ref} from "vue";
export default {
  name: "TodoItem",
  props:['todoProps'],
  setup(props, context) {
    const markItemCompleted = () => {
      console.log(props.todoProps)
      context.emit('item-completed',props.todoProps.id)
    }
     const deleteItem = () => {
       context.emit('delete-item',props.todoProps.id)
     }
    return {
      markItemCompleted,
      deleteItem
    }
  }

}
</script>

<style scoped>

.todo-items{
  background: #f4f4f4;
  padding: 10px;
  margin: 10px;
  border-bottom: 1px #ccc dotted;
}

.is-completed{
  text-decoration-line: line-through;
}
.del-btn{
  background: #ff0000;
  color: #fff;
  border: none;
  cursor: pointer;
  float: right;
}
</style>

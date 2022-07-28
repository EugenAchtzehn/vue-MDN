<template>
  <div id="app">
    <h1>To-do list</h1>
    <!-- <input type="text" name="inputText" id="inputText" v-model="labelText" /> -->
    <to-do-form @todo-added="addToDo"></to-do-form>
    <ul>
      <li v-for="item in ToDoItems" :key="item.id">
        <!-- 父層傳給子層用 props -->
        <!-- <componentTag :title="item.title" :img="item.imgUrl" /> -->
        <to-do-item :label="item.label" :done="item.done" :id="item.id"></to-do-item>
      </li>
    </ul>
  </div>
</template>

<script>
import ToDoItem from '@/components/ToDoItem.vue';
import ToDoForm from '@/components/ToDoForm.vue';
import uniqueId from 'lodash.uniqueid';

export default {
  name: 'App',
  components: {
    ToDoItem,
    ToDoForm,
  },
  data() {
    return {
      // labelText: 'testing',
      // 利用 lodash 套件來附加 UID 功能
      ToDoItems: [
        { id: uniqueId('todo-'), label: 'Learn Vue', done: false },
        { id: uniqueId('todo-'), label: 'Create a Vue project with CLI', done: true },
        { id: uniqueId('todo-'), label: 'Have fun', done: false },
        { id: uniqueId('todo-'), label: 'Complete a to-do list', done: true },
      ],
    };
  },
  methods: {
    addToDo(toDoInput) {
      console.log('emit success!, inputVal:', toDoInput);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

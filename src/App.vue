<template>
  <div id="container">
    <h1>Eugene's To-Do List</h1>

    <!-- <input type="text" name="inputText" id="inputText" v-model="labelText" /> -->

    <to-do-form @todo-added="addToDo"></to-do-form>
    <h2 id="todo-summary">{{ todoSummary }}</h2>
    <ul class="stack-large" aria-labelledby="todo-summary">
      <li v-for="item in ToDoItems" :key="item.id">
        <!-- 父層傳給子層用 props -->
        <!-- <componentTag :title="item.title" :img="item.imgUrl" /> -->
        <to-do-item
          :label="item.label"
          :done="item.done"
          :id="item.id"
          @checkbox-changed="updateDoneStatus(item.id)"
          @item-deleted="deleteTodo(item.id)"
          @item-edited="editTodo(item.id, $event)"
        ></to-do-item>
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
        { id: uniqueId('todo-'), label: '開啟一個 Vue 專案', done: true },
        { id: uniqueId('todo-'), label: '學習 Vue3', done: false },
        { id: uniqueId('todo-'), label: 'Have fun', done: false },
        { id: uniqueId('todo-'), label: '回台中', done: false },
      ],
    };
  },
  methods: {
    addToDo(toDoInput) {
      // console.log('emit success!, inputVal:', toDoInput);
      // 將 emit 的送出推送到代辦陣列中
      this.ToDoItems.push({ id: uniqueId('todo-'), label: toDoInput, done: false });
    },
    updateDoneStatus(todoId) {
      const todoUpdate = this.ToDoItems.find((item) => {
        return item.id === todoId;
      });
      // toggle status
      // console.log(todoUpdate);
      todoUpdate.done = !todoUpdate.done;
    },
    deleteTodo(todoId) {
      const itemIndex = this.ToDoItems.findIndex((item) => {
        return item.id === todoId;
      });
      this.ToDoItems.splice(itemIndex, 1);
    },
    editTodo(todoId, newLabel) {
      // console.log('emit event: ', newLabel);
      const todoToEdit = this.ToDoItems.find((item) => {
        return item.id === todoId;
      });
      todoToEdit.label = newLabel;
    },
  },
  computed: {
    todoSummary() {
      const numCompletedItems = this.ToDoItems.filter((item) => {
        return item.done === true;
      }).length;
      return `${this.ToDoItems.length} 項任務已有 ${numCompletedItems} 項完成`;
    },
  },
};
</script>

<style>
/* #root {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */

/* Global styles */
.btn {
  padding: 0.8rem 1rem 0.7rem;
  border: 0.2rem solid #4d4d4d;
  cursor: pointer;
  text-transform: capitalize;
}
.btn__danger {
  color: #fff;
  background-color: #ca3c3c;
  border-color: #bd2130;
}
.btn__filter {
  border-color: lightgrey;
}
.btn__danger:focus {
  outline-color: #c82333;
}
.btn__primary {
  color: #fff;
  background-color: #000;
}
.btn-group {
  display: flex;
  justify-content: space-between;
}
.btn-group > * {
  flex: 1 1 auto;
}
.btn-group > * + * {
  margin-left: 0.8rem;
}
.label-wrapper {
  margin: 0;
  flex: 0 0 100%;
  text-align: center;
}
[class*='__lg'] {
  display: inline-block;
  width: 100%;
  font-size: 1.9rem;
}
[class*='__lg']:not(:last-child) {
  margin-bottom: 1rem;
}
@media screen and (min-width: 620px) {
  [class*='__lg'] {
    font-size: 2.4rem;
  }
}
.visually-hidden {
  position: absolute;
  height: 1px;
  width: 1px;
  overflow: hidden;
  clip: rect(1px 1px 1px 1px);
  clip: rect(1px, 1px, 1px, 1px);
  clip-path: rect(1px, 1px, 1px, 1px);
  white-space: nowrap;
}
[class*='stack'] > * {
  margin-top: 0;
  margin-bottom: 0;
}
.stack-small > * + * {
  margin-top: 1.25rem;
}
.stack-large > * + * {
  margin-top: 2.5rem;
}
@media screen and (min-width: 550px) {
  .stack-small > * + * {
    margin-top: 1.4rem;
  }
  .stack-large > * + * {
    margin-top: 2.8rem;
  }
}
/* End global styles */
#container {
  background: #fff;
  margin: 2rem 0 4rem 0;
  padding: 1rem;
  padding-top: 0;
  position: relative;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 2.5rem 5rem 0 rgba(0, 0, 0, 0.1);
}
@media screen and (min-width: 550px) {
  #container {
    padding: 4rem;
  }
}
#container > * {
  max-width: 50rem;
  margin-left: auto;
  margin-right: auto;
}
#container > form {
  max-width: 100%;
}
#container h1 {
  display: block;
  min-width: 100%;
  width: 100%;
  text-align: center;
  margin: 0;
  margin-bottom: 1rem;
}
</style>

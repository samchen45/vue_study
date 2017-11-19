<template>
  <div id="todoList">
    <h1>Todo List</h1>
    <!--deal with the todos we want to add-->
    <todo-add v-on:add="addTodo"></todo-add>
    <!--deal with the status of todos-->
    <ul class="todos">
      <li v-for="todo, index in todos" class="todo">
        <!--click on the checkbox to make the todo finished-->
        <input
          type="checkbox"
          name=""
          value=""
          :checked="todo.isFinished"
          @click="finished (index)"
        >
        </input>
        <!--click on the todo to make the todo finished-->
        <span
          :class="todo.isFinished ? 'finished' : ''"
          @click="finished (index)"
        >
          <em>{{ index }}.</em>{{ todo.text }}
        </span>
      </li>
    </ul>
    <div>
      <p v-show="todos.length === 0">
        Congraduations! All things have been finished!
      </p>
      <p v-show="todos.length !== 0">
        {{ count_finished }} things has been finished. 
        {{ count_n_finished }} things waiting to be finished in <strong>{{ todos.length }}</strong> things
      </p>
    </div>
  </div>
</template>
<script>
import TodoAdd from './TodoAdd.vue'
export default {
  name: 'TodoList',
  components: {
    TodoAdd
  },
  data: () => ({
    // use array to save todos, here i use some examples to show the web
    todos: [{
      text: '吃',
      isFinished: true
    }, {
      text: '睡觉',
      isFinished: false
    }, {
      text: '学习',
      isFinished: false
    }]
  }),
  methods: {
    // deal with the status of todos
    finished: function (index) {
      this.todos[index].isFinished = !this.todos[index].isFinished
    },
    // add new todo
    addTodo: function (todo) {
      this.todos.push({
        text: todo,
        isFinished: false
      })
    }
  },
  computed: {
    count_finished: function () {
      return this.todos.filter(item => item.isFinished).length
    },
    count_n_finished: function () {
      return this.todos.filter(item => !item.isFinished).length
    }
  }
}
</script>
<style scoped>
#todoList {
  margin: 0 auto;
  max-width: 400px;
}

.todos li {
  list-style: none;
}

.todo {
  text-align: left;
  cursor: pointer;
}

.finished {
  text-decoration: line-through;
}

</style>
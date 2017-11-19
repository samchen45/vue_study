<template>
  <div id="todoList">
    <h1>Todo List</h1>
    <!--deal with the todos we want to add-->
    <todo-add v-on:add="addTodo"></todo-add>
    <ul class="todos">
      <li v-for="todo, index in todos" class="todo">
        <input
          type="checkbox"
          name=""
          value=""
          :checked="todo.isFinished"
          @click="finished (index)"
        >
        </input>
        <span
          :class="todo.isFinished ? 'finished' : ''"
          @click="finished (index)"
        >
          <em>{{ index }}.</em>{{ todo.text }}
        </span>
      </li>
    </ul>
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
    // use array to save todos
    todos: [{
      text: '吃',
      isFinished: false
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
  }
}
</script>
<style scoped>
#todoList {
  margin: 0 auto;
  max-width: 350px;
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
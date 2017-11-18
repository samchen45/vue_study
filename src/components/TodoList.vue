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
          :checked="todo.isfinished"
          @click="finished (index)" 
        >
        <span
          :class="todo.isfinished ? 'finished' : ''"
          @click="finished (index)"   
        >
          <em>{{ index }}.</em>{{ todo.text }}
        </span>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'TodoList',
  data: () => ({
    // use array to save todos
    todos: [{
      text: '吃饭',
      isfinished: false
    }, {
      text: '睡觉',
      isfinished: false
    }, {
      text: '学习',
      isfinished: false
    }]
  }),
  methods: {
    // deal with the status of todos
    finished (index) {
      this.todos[index].isfinished = !this.todos[index].isfinished
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
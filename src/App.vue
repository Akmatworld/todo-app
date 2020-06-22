<template>
  <div id="app">
    <Todos :todos="todos" @delete-todo="deleteTodo"/>
    <AddTodo @add-todo="addTodo"/>
  </div>
</template>
<script>
import Todos from './components/Todos'
import AddTodo from './components/AddTodo'

export default {
  name: 'App',
  components: {
    Todos,
    AddTodo
  },
  data () {
    return {
      todos: [
        {
          id: 1,
          title: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Inventore repellat, a odio eius at necessitatibus, quibusdam, possimus quae cum maiores rerum quasi odit culpa. Earum minima error minus eveniet consequatur.',
          completed: false
        },
        {
          id: 2,
          title: 'Do laundry',
          completed: false
        },
        {
          id: 3,
          title: 'Cook food',
          completed: false
        },
        {
          id: 4,
          title: 'Clean up room',
          completed: false
        },
        {
          i: 5,
          title: 'Finish work',
          completed: false
        }
      ]
    }
  },
  methods: {
    addTodo (newTodoObj) {
      this.todos = [...this.todos, newTodoObj]
    },
    deleteTodo (todoId) {
      this.todos = this.todos.filter(todo => todo.id !== todoId)
    }
  }
}
</script>

<style lang="scss">
body {
  margin: 0;
  paddin: 0;
}
#app {
  border: 1px solid #ccc;
  width: 80%;
  margin: 0 auto;
}
</style>

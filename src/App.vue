<template>
  <div id="app">
    <h2 class="todo-title">My todolist</h2>
    <AddTodo @add-todo="addTodo"/>
    <Todos :todos="todos" @delete-todo="deleteTodo" @save-text="saveText"/>
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
          title: 'Lorem ipsum dolor sit amet consectetur adipisicing elit.Earum minima error minus eveniet consequatur.',
          completed: false
        },
        {
          id: 2,
          title: 'Inventore repellat, a odio eius at necessitatibus',
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
          title: 'Earum minima error minus eveniet consequatur.',
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
    },
    saveText (changedText) {
      this.todos.forEach((item, index) => {
        if (item.id === changedText.id) {
          this.todos[index].title = changedText.title
        }
      })
    }
  }
}
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
}
#app {
  width: 80%;
  margin: 0 auto;
  border: 1px solid #ccc;
}
.todo-title {
  text-align: center;
  margin:10px 0 20px;
}
</style>

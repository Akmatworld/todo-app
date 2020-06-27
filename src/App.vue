<template>
  <div id="app">
    <h2 class="todo-title">Personal</h2>
    <AddTodo @add-todo="addTodo"/>
    <Todos :todos="todos" :hideText="isHidetext" :title-hide-or-show="titleHideOrShow" :completed-todos="completedTodos" @delete-todo="deleteTodo" @save-text="saveText" @move-text-completed="moveText" @move-text-Back="moveBack" @hide-completed-tasks="hideCompletedTasks"/>
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
          id: 5,
          title: 'Earum minima error minus eveniet consequatur.',
          completed: false
        }
      ],
      completedTodos: [],
      temporaryComletedTasks: [],
      isHidetext: false,
      titleHideOrShow: 'Hide '
    }
  },
  methods: {
    addTodo (newTodoObj) {
      this.todos = [...this.todos, newTodoObj]
    },
    deleteTodo (todoId) {
      this.completedTodos = this.completedTodos.filter(ctodo => ctodo.id !== todoId)
      if (this.completedTodos.length === 0) {
        this.isHidetext = false
      }
    },
    saveText (changedText) {
      this.todos.forEach((item, index) => {
        if (item.id === changedText.id) {
          this.todos[index].title = changedText.title
        }
      })
    },
    hideCompletedTasks () {
      if (this.completedTodos.length > 0) {
        this.temporaryComletedTasks = this.completedTodos
        this.completedTodos = []
        this.titleHideOrShow = 'Show '
      } else {
        this.completedTodos = this.temporaryComletedTasks
        this.temporaryComletedTasks = []
        this.titleHideOrShow = 'Hide '
      }
    },
    moveText (id) {
      this.isHidetext = true
      let index = null
      this.todos.forEach((item, i) => {
        if (item.id === id) {
          index = i
          item.completed = true
          this.completedTodos.push(item)
        }
      })
      this.todos.splice(index, 1)
    },
    moveBack (id) {
      let index = null
      this.completedTodos.forEach((item, i) => {
        if (item.id === id) {
          index = i
          item.completed = false
          this.todos.push(item)
        }
      })
      this.completedTodos.splice(index, 1)
      if (this.completedTodos.length === 0) {
        this.isHidetext = false
      }
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
  width: 70%;
  margin: 0 auto 50px;
  font-family: Roboto;
}
.todo-title {
  text-align: center;
  margin:10px 0 20px;
  color: #45c7c1;
  font-weight: 900;
}
@media only screen and (max-width: 913px) {
  .todo-title {
    font-size: 28px;
    margin: 10px 0;
  }
}
@media only screen and (max-width: 500px) {
  #app {
    width: 100%;
  }
}
</style>

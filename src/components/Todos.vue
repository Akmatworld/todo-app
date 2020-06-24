<template>
  <div>
    <ul class="todos-ul">
      <li v-bind:key="todo.id" v-for="todo in todos">
        <Todo v-bind:todo="todo" @delete-todo="$emit('delete-todo', todo.id)" @save-text="saveText"/>
      </li>
    </ul>
  </div>
</template>
<script>
import Todo from './Todo'

export default {
  name: 'Todos',
  components: {
    Todo
  },
  props: [
    'todos'
  ],
  methods: {
    saveText (changedText) {
      this.$emit('save-text', changedText)
    }
  }
}
</script>
<style scoped lang="scss">
.todos-ul {
  padding: 0 10px;
}
.todos-ul li {
  list-style-type: none;
}
</style>

<template>
  <div>
    <ul class="todos-ul">
      <li :key="todo.id" v-for="todo in todos">
        <Todo :todo="todo" @save-text="saveText" @move-text-completed="moveText"/>
      </li>
      <HideCompletedTasksBtn v-if="hideText" :title="titleHideOrShow" @hide-completed-tasks="$emit('hide-completed-tasks')"/>
      <li :key="ctodo.id" v-for="ctodo in completedTodos">
        <CompletedTodo :ctodo="ctodo" @delete-todo="$emit('delete-todo', ctodo.id)" @move-back="$emit('move-text-Back', ctodo.id)"/>
      </li>
    </ul>
  </div>
</template>
<script>
import Todo from './Todo'
import CompletedTodo from './completedTodo'
import HideCompletedTasksBtn from './HideCompletedTasksButton'

export default {
  name: 'Todos',
  components: {
    Todo,
    CompletedTodo,
    HideCompletedTasksBtn
  },
  props: [
    'todos',
    'completedTodos',
    'hideText',
    'titleHideOrShow'
  ],
  methods: {
    saveText (changedText) {
      this.$emit('save-text', changedText)
    },
    moveText (id) {
      this.$emit('move-text-completed', id)
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

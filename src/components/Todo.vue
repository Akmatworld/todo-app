<template>
  <div>
    <div :class="{ 'completed': todo.completed }">
      <p @click="markComplete">{{ todo.title }}</p>
      <button @click="$emit('delete-todo', todo.id)">Delete</button>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Todo',
  props: [
    'todo'
  ],
  methods: {
    markComplete () {
      this.todo.completed = !this.todo.completed
    }
  }
}
</script>
<style scoped>
  .completed {
    text-decoration: line-through;
  }
</style>

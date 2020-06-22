<template>
  <div>
    <div :class="{ 'completed': todo.completed }">
      <div class="item-div">
        <button @click="markComplete">Done</button>
        <button @click="$emit('delete-todo', todo.id)">Delete</button>
        <p class="item-p" :class="{completed: isActive}">{{ todo.title }}</p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Todo',
  data () {
    return {
      isActive: false
    }
  },
  props: [
    'todo'
  ],
  methods: {
    markComplete () {
      this.isActive = this.isActive === false
    }
  }
}
</script>
<style scoped>
  .completed {
    text-decoration: line-through;
  }
  .item-p {
    border: 1px solid #ccc;
    padding: 0 5px;
    font-size: 25px;
  }
  .item-div {
    display:flex;
    margin-bottom: 20px;
    border: 1px solid #ccc;
  }
</style>

<template>
  <div>
    <div :class="{ 'completed': todo.completed }">
      <div class="item-div">
        <b-button class="done" @click="markComplete" variant="success">Done</b-button>
        <b-button class="delete" @click="$emit('delete-todo', todo.id)" variant="danger">Delete</b-button>
        <p class="item-p" :class="{completed: isActive}">{{ todo.title }}</p>
      </div>
      <div class="change-text">
        <input type="text" :value="todo.title">
      </div>
    </div>
  </div>
</template>
<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

export default {
  name: 'Todo',
  data () {
    return {
      isActive: false,
      text: this.todo.title
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
<style scoped lang="scss">
  .completed {
    text-decoration: line-through;
    color: #ccc;
  }
  .item-p {
    /* border: 1px solid #ccc; */
    padding: 0 5px;
    font-size: 25px;
    width: 100%;
    margin: 0;
    border-top: 1px solid #ccc;
  }
  .item-div {
    display:flex;
    margin-bottom: 20px;
    padding: 3px 0 3px 5px;
    &:hover {
      border-radius: 3px;
    }
  }
  .done {
    width: 10%;
    margin-right: 5px;
    height: 40px;
  }
  .delete {
    width: 10%;
    margin-right: 5px;
    height: 40px;
  }
</style>

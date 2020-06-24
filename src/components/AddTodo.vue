<template>
  <div>
    <h2 :class="{'hide-error': isError}" class="error">{{ errorText }}</h2>
    <div class="add-todo-item">
      <input type="text" v-model="title" name="title" @keyup.esc="clean" @keyup.enter="addTodo" class="form-control add-input" placeholder="Enter text that add in to the todo list">
      <b-button type="submit" variant="outline-primary" @click="addTodo" class="add-btn">Add</b-button>
    </div>
  </div>
</template>

<script>
import { uuid } from 'vue-uuid'

export default {
  name: 'AddTodo',
  data () {
    return {
      title: '',
      errorText: '',
      isError: true
    }
  },
  methods: {
    addTodo (e) {
      if (this.title) {
        const newTodoObj = {
          id: uuid.v4(),
          title: this.title,
          completed: false
        }
        this.$emit('add-todo', newTodoObj)
        this.title = ''
      } else {
        this.errorText = 'Input is empty!'
        this.isError = false
        setTimeout(() => {
          this.isError = true
        }, 2000)
      }
    },
    clean (e) {
      e.target.value = ''
    }
  }
}
</script>

<style scoped lang="scss">
.add-todo-item {
  margin: 0 0 20px;
  display: flex;
  justify-content:space-between;
}
.add-input {
  margin: 0 10px;
  display: inline-block;
  width: 100%;
}
.add-btn {
  width: 100px;
  margin-right: 5px;
  height: 37px;
}
.error {
  color: red;
  padding: 3px 10px;
  margin: 10px 10px 10px;
  font-size: 20px;
}
.hide-error {
  display: none;
}
</style>

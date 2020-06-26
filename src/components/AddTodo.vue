<template>
  <div>
    <h2 :class="{'hide-error': isError}" class="error">{{ errorText }}</h2>
    <div class="add-todo-item">
      <div @click="addTodo" class="add-btn-icon">
        <i class="fas fa-plus add-btn-icon"></i>
      </div>
      <input type="text" v-model="title" name="title" @keyup.esc="clean" @keyup.enter="addTodo" class="form-control add-input" placeholder="Add task...">
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
        this.errorText = 'Input is empty! Please enter text to add.'
        this.isError = false
        setTimeout(() => {
          this.isError = true
        }, 3000)
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
  position: relative;
}
.add-input {
  margin: 0 10px;
  display: inline-block;
  width: 100%;
  background-color: #eaebed;
  padding: 0 0 0 40px;
  color: rgb(44, 36, 36);
  font-family: Roboto;
  font-size: 20px;
}
.add-btn-icon {
  position: absolute;
  top: 5px;
  left: 10px;
  font-size: 23px;
  color: #000;
  font-weight: 100;
  &:hover {
    cursor: pointer;
  }
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
@media only screen and (max-width: 913px) {
  .add-input {
    margin: 0 10px;
    font-size: 17px;
  }
  .add-btn-icon {
    position: absolute;
    top: 5px;
    left: 11px;
    font-size: 20px;
  }
}
</style>

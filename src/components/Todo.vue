<template>
  <div>
    <div :class="{ 'completed': todo.completed }">
      <div class="item-div">
        <div class="save" :class="{hide: isChange}" @click="saveText">
          <i class="far fa-save save-icon"></i>
        </div>
        <div class="cancel" :class="{hide: isChange}" @click="cancel">
          <i class="far fa-times-circle cancel-icon"></i>
        </div>
        <div class="completed-container">
          <input type="checkbox" class="completed-checkbox" :class="{hideEdit: isEdit}" v-model="isCompleted">
        </div>
        <p class="item-p" :class="{completed: isCompleted, hide: isHide}">{{ todo.title }}</p>
        <!-- <div class="trash-icon" @click="$emit('delete-todo', todo.id)">
          <i class="far fa-trash-alt"></i>
        </div> -->
        <div class="form-group item-p" :class="{hide: isChange}">
          <h2 class="error" :class="{hide: isError}">{{ errorText }}</h2>
          <input type="text" v-model="text" name="title"  ref="changeText" @keyup.esc="cancel" @keyup.enter="saveText" class="form-control edit-input" placeholder="Edit...">
        </div>
        <div class="pen-icon" :class="{hideEdit: isEdit}" @click="clickChangeText">
          <i class="fas fa-pen"></i>
        </div>
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
      isHide: false,
      isChange: true,
      isCompleted: false,
      isError: true,
      isEdit: false,
      errorText: 'To change you need enter change text!',
      text: this.todo.title,
      id: this.todo.id
    }
  },
  props: [
    'todo'
  ],
  methods: {
    markComplete () {
      this.isCompleted = this.isCompleted === false
    },
    clickChangeText () {
      this.isHide = true
      this.isChange = false
      this.isEdit = true
      console.log(this)
      this.$nextTick(() => {
        this.$refs.changeText.focus()
      })
    },
    saveText () {
      if (this.text.length > 0) {
        this.$emit('save-text', { title: this.text, id: this.id })
        this.isHide = false
        this.isChange = true
        this.isEdit = false
      } else {
        this.isError = false
        setTimeout(() => {
          this.isError = true
        }, 2000)
      }
    },
    cancel () {
      this.isHide = false
      this.isChange = true
      this.isEdit = false
      this.text = this.todo.title
    }
  }
}
</script>
<style scoped lang="scss">
  $iconColor: #000;
  .completed-checkbox {
    margin: 10px 4px 0 0;
    &:hover {
      cursor: pointer;
    }
  }
  .completed {
    text-decoration: line-through;
    color: #ccc;
  }
  .item-p {
    padding: 0 5px;
    font-size: 20px;
    width: 100%;
    margin: 0;
  }
  .form-control {
    font-size: 25px;
  }
  .item-div {
    display:flex;
    padding: 3px 0 3px 0;
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
  .edit-input {
    font-size: 20px;
    padding: 0 4px;
  }
  .hide, .hideEdit {
    display: none;
  }
  .save {
    width: 3%;
    margin: 10px 7px 0 0;
  }
  .cancel {
    width: 3%;
    margin: 10px 7px 0 0;
  }
  .error {
    font-size: 20px;
    color: red;
  }
  .pen-icon, .trash-icon, .cancel-icon, .save-icon {
    color: $iconColor;
    height: 20px;
    width: 20px;
    font-size: 20px;
    &:hover {
      cursor: pointer;
    }
  }
  @media only screen and (max-width: 449px) {
    .item-div {
      padding-left: 0;
    }
    .done,
    .delete,
    .cancel,
    .save {
      width: 16%;
      margin: 6px 0 0 0;
    }
    .done {
      margin-right: 10%;
    }
    .item-p {
      font-size: 18px;
    }
    .edit-input {
      font-size: 15px;
    }
  }
  @media only screen and (min-width: 440px) and (max-width: 639px) {
    .item-div {
      padding-left: 0;
    }
    .done,
    .delete,
    .cancel,
    .save {
      width: 10%;
      margin: 6px 0 0 0;
    }
    .done {
      margin-right: 10%;
    }
    .item-p {
      font-size: 18px;
    }
    .edit-input {
      font-size: 15px;
    }
  }
  @media only screen and (min-width: 640px) and (max-width: 913px) {
    .item-div {
      padding-left: 0;
    }
    .done,
    .delete,
    .cancel,
    .save {
      width: 6%;
      margin: 6px 0 0 0;
    }
    .done {
      margin-right: 10%;
    }
    .item-p {
      font-size: 18px;
      width: 100%;
    }
    .edit-input {
      font-size: 15px;
    }
  }
  @media only screen and (max-width: 913px) {
    .item-div {
      padding-left: 0;
      margin-bottom: 0;
    }
  }
</style>

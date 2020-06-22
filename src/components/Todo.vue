<template>
  <div>
    <div :class="{ 'completed': todo.completed }">
      <div class="item-div">
        <b-button class="done" :class="{hide: isHide}" @click="markComplete" variant="success">Done</b-button>
        <b-button class="delete" :class="{hide: isHide}" @click="$emit('delete-todo', todo.id)" variant="danger">Delete</b-button>
        <b-button class="save" :class="{hide: isChange}" @click="saveText" variant="outline-primary">Save</b-button>
        <p class="item-p" :class="{completed: isCompleted, hide: isHide}" @click="clickChangeText">{{ todo.title }}</p>
        <div class="form-group item-p" :class="{hide: isChange}">
          <textarea class="form-control" id="changeTextId" rows="3" v-model='text'></textarea>
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
    },
    saveText () {
      this.$emit('save-text', { title: this.text, id: this.id })
      this.isHide = false
      this.isChange = true
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
  .hide {
    display: none;
  }
</style>

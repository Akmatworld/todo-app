<template>
  <div>
    <div :class="{ 'completed': isCompleted }">
      <div class="item-div">
        <div class="completed-container">
          <input type="checkbox" class="completed-checkbox" v-model="isCompleted">
        </div>
        <p class="item-p" :class="{completed: isCompleted}">{{ ctodo.title }}</p>
        <div class="trash-icon" @click="$emit('delete-todo')">
          <i class="far fa-trash-alt"></i>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'completedTodo',
  props: ['ctodo'],
  data () {
    return {
      isCompleted: this.ctodo.completed
    }
  },
  watch: {
    isCompleted (val, oldVal) {
      this.$emit('move-back')
    }
  }
}
</script>
<style scoped lang="scss">
</style>

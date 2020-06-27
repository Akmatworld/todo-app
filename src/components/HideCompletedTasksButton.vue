<template>
  <div class="hide-completed-list">
    <div class="hide-completed-bnt" @click="hideCompletedTasks">{{ title }}Completed Tasks</div>
  </div>
</template>
<script>
export default {
  name: 'HideCompletedTasksButton',
  props: ['title'],
  methods: {
    hideCompletedTasks () {
      this.$emit('hide-completed-tasks')
    }
  }
}
</script>
<style lang="scss" scoped>
  .hide-completed-list {
    display: flex;
    justify-content: center;
  }
  .hide-completed-bnt {
    display: inline-block;
    background-color: #45c7c1;
    color: #fff;
    border-radius: 5px;
    padding: 0 10px 0;
    &:hover {
      cursor: pointer;
    }
  }
</style>

<template lang="">
  <div class="task" :class="stateClass" @click="$emit('taskStateChanged', task)">
    <span @click.stop="$emit('taskDeleted', task)" class="close">x</span>
    <p>{{ task.name }}</p>
  </div>
</template>
<script>
export default {
  props: {
    task: {
      type: Object,
      required: true,
    }
  },
  computed: {
    stateClass() {
      return {
        pending: this.task.isPending,
        done: !this.task.isPending,
      }
    }
  }
}
</script>
<style scoped>
  .task {
    position: relative;
    box-sizing: border-box;
    width: 350px;
    height: 150px;
    padding: 10px;
    border-radius: 8px;
    cursor: pointer;
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .task p {
    font-size: 2rem;
    font-weight: 300;
  }
  .pending {
    border-left: 12px solid #B73229;
    background-color: #F44336;
  }
  .done {
    color: #DDD;
    border-left: 12px solid #0A8F08;
    background-color: #4CAF50;
    text-decoration-line: line-through;
  }
  .pending .close {
    background: #B73229;
  }
  .done .close {
    background: #0A8F08;
  }
  .close {
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 0.9rem;
    font-weight: bold;
    height: 20px;
    width: 20px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
  }
</style>
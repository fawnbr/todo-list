<template>
  <div class="task-grid">
    <template v-if="tasks.length">
      <Task
      v-for="(task, id) in tasks"
      :key="task.name"
      :task="task"
      @taskDeleted="$emit('taskDeleted', id)"
      @taskStateChanged="$emit('taskStateChanged', id)"
      />    
    </template>
    <template v-else>
      <p class="no-tasks">You are up to date.</p>
    </template>
  </div>
</template>
<script>
import Task from '../Task';
export default {
  components: {Task},
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
};
</script>
<style scoped>
  .task-grid {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
  }
  .task-grid .task {
    margin: 10px;
  }
  .no-tasks {
    font-size: 1.7rem;
    color: #AAA;
  }

</style>
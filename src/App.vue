<template>
	<div id="app">
		<h1>Tasks</h1>
    <TaskProgress :progress="progress" />
    <NewTask @taskAdded="addTask"/>
    <TaskGrid
      :tasks="tasks"
      @taskDeleted="deleteTask"
      @taskStateChanged="toggleTaskState"
    />	
  </div>
</template>

<script>
  import TaskProgress from './components/TaskProgress';
  import NewTask from './components/NewTask';
  import TaskGrid from './components/TaskGrid';
export default {
  components: { TaskProgress, NewTask, TaskGrid },
  data() {
    return {
      tasks: [],
    }
  },
  computed: {
    progress() {
      const total = this.tasks.length;
      const finishedTasks = this.tasks.filter(t => !t.isPending).length;
      return Math.round((finishedTasks / total) *100) || 0;
    }
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
         localStorage.setItem('tasks', JSON.stringify(this.tasks));
      }
    }
  },
  methods: {
    addTask(task) {
      const isSameName = t => t.name === task.name;
      const isNewTask = this.tasks.filter(isSameName).length == 0;
      isNewTask && this.tasks.push({
        name: task.name,
        isPending: true,
      });
    },
    deleteTask(id){
      this.tasks.splice(id, 1);
    },
    toggleTaskState(id){
      this.tasks[id].isPending = !this.tasks[id].isPending;
    }
  },
  created() {
    const json = localStorage.getItem('tasks');
    this.tasks = JSON.parse(json) || [];
  }
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>

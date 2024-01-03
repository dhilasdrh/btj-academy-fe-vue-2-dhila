<template>
    <div class="grid md:grid-cols-2">
      <div class="py-5 px-4 bg-slate-100 mx-4 my-5 rounded-lg">
        <TaskList title="To Do" :tasks="todoTasks" :emptyMessage="todoEmptyMessage" @deleteTask="deleteTask" @markAsDone="markAsDone" />
      </div>
      <div class="py-5 px-4 bg-slate-100 mx-4 my-5 rounded-lg">
        <TaskList title="Done" :tasks="completedTasks" :emptyMessage="completedEmptyMessage" @deleteTask="deleteTask" />
      </div>
    </div>
  </template>
  
  <script>
  import TaskList from './TaskList.vue';
  
  export default {
    components: {
      TaskList,
    },
    props: {
      todoTasks: Array,
      completedTasks: Array,
      todoEmptyMessage: String,
      completedEmptyMessage: String,
    },
    methods: {
      deleteTask(idTask) {
        this.$emit('deleteTask', idTask);
      },
      markAsDone(idTask) {
        this.$emit('markAsDone', idTask);
      },
    },
  };
  </script>
  
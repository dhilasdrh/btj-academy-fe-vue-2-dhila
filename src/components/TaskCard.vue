<!-- TaskCard.vue -->
<template>
  <div class="flex justify-between bg-white/80 p-4 mt-3 border-slate-200 border rounded-lg">
    <div> 
      <p class="text-lg font-semibold mb-2">{{ task.name }}</p>
      <div :class="[getPriorityColorClass(task.priority), 'flex items-center rounded-2xl py-1 px-3 bg-opacity-40']">
        <div :class="[getPriorityColorClass(task.priority), 'w-3 h-3 rounded-full mr-2']"></div>
        <span class="text-xs font-bold text-gray-700 uppercase">{{ task.priority }}</span>
      </div>
    </div>
    <div class="flex items-center gap-3">
      <button @click="deleteTask" class="text-sm bg-red-500/80 rounded-sm px-3 py-2 text-white shadow-md shadow-red-500/20 transition-all hover:shadow-lg hover:shadow-red-500/40">Delete</button>
      <button v-if="!task.completed" @click="markAsDone" class="text-sm bg-green-500/80 rounded-sm px-3 py-2 text-white shadow-md shadow-green-500/20 transition-all hover:shadow-lg hover:shadow-green-500/40">Done</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    task: Object,
  },
  methods: {
    deleteTask() {
      this.$emit('deleteTask', this.task.idTask);
    },
    markAsDone() {
      this.$emit('markAsDone', this.task.idTask);
    },
    getPriorityColorClass(priority) {
      switch (priority) {
        case "Low":
          return "bg-blue-500";
        case "Medium":
          return "bg-yellow-500";
        case "High":
          return "bg-red-500";
        default:
          return "bg-gray-500";
      }
    },
  },
};
</script>
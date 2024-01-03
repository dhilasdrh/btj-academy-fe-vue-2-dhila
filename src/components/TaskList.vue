<template>
  <div>
    <h3 class="text-2xl text-gray-800 font-medium">{{ title }}</h3>
    <div v-if="tasks.length === 0">
      <p class="py-5">{{ emptyMessage }}</p>
    </div>
    <div v-else>
      <TaskCard
        v-for="task in tasks"
        :key="task.idTask"
        :task="task"
        @deleteTask="onDeleteTask"
        @markAsDone="onMarkAsDone"
      />
    </div>
  </div>
</template>

<script>
import TaskCard from './TaskCard.vue';

export default {
  props: {
    title: {
      type: String,
      required: true,
      validator: (value) => value.length > 0, // custom validation
    },
    tasks: {
      type: Array,
      default: () => [],
    },
    emptyMessage: {
      type: String,
      default: 'No tasks available.',
    },
  },
  components: {
    TaskCard,
  },
  methods: {
    onDeleteTask(idTask) {
      this.$emit('delete-task', idTask);
    },
    onMarkAsDone(idTask) {
      this.$emit('mark-as-done', idTask);
    },
  },
  watch: {
    tasks: {
      handler(newTasks, oldTasks) {
        console.log('Tasks updated:', newTasks);
      },
      deep: true,
    },
  },
  created() {
    console.log('TaskList created');
  },
  mounted() {
    console.log('TaskList mounted');
  },
  beforeDestroy() {
    console.log('TaskList beforeDestroy');
  },
};
</script>

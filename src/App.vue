<template>
  <BaseLayout>
    <template v-slot:header>
        <HeaderSection />
      </template>

      <template v-slot:summary>
        <SummarySection
          :totalPendingTask="totalPendingTask"
          :totalLowPriorityTask="totalLowPriorityTask"
          :totalMediumPriorityTask="totalMediumPriorityTask"
          :totalHighPriorityTask="totalHighPriorityTask"
        />
      </template>

      <template #addTask>
        <AddTaskSection
          @new-task="addNewTask"
          :showErrorMessage="errorMessage"
          :showSuccessMessage="successMessage"
        />
      </template>

      <template #taskList>
        <TaskListSection 
          :todoTasks="todoTasks" 
          :completedTasks="completedTasks" 
          @deleteTask="deleteTask" 
          @markAsDone="markAsDone" />
      </template>

      <template #footer> 
        <FooterSection />
      </template>
  </BaseLayout>
</template>

<script>
import BaseLayout from './layouts/BaseLayout.vue';
import HeaderSection from './components/HeaderSection.vue'
import SummarySection from './components/SummarySection.vue';
import AddTaskSection from './components/AddTaskSection.vue';
import TaskListSection from './components/TaskListSection.vue';
import FooterSection from './components/FooterSection.vue';

export default {
  components: {
    BaseLayout,
    HeaderSection,
    SummarySection,
    AddTaskSection,
    TaskListSection,
    FooterSection,
  },
  data() {
    return {
      counter: 0,
      tasks: this.getStoredTasks(),
      errorMessage: false,
      successMessage: false,
    };
  },
  computed: {
    todoTasks() {
      return this.tasks.filter(task => !task.completed);
    },
    completedTasks() {
      return this.tasks.filter(task => task.completed);
    },
    totalPendingTask() {
      return this.todoTasks.length;
    },
    totalLowPriorityTask() {
      return this.todoTasks.filter(task => task.priority === 'Low').length;
    },
    totalMediumPriorityTask() {
      return this.todoTasks.filter(task => task.priority === 'Medium').length;
    },
    totalHighPriorityTask() {
      return this.todoTasks.filter(task => task.priority === 'High').length;
    },
  },
  methods: {
    addNewTask(newTask) {
        newTask.idTask = this.counter;
        this.tasks.push(newTask);
        this.counter += 1;
        this.updateLocalStorage();
    },
    showErrorMessage(message) {
      this.errorMessage = true;
      this.$nextTick(() => {
        this.errorMessage = false;
      });
    },
    showSuccessMessage(message) {
      this.successMessage = true;
      this.$nextTick(() => {
        this.successMessage = false;
      });
    },
    deleteTask(idTask) {
        let index = this.tasks.findIndex(task => task.idTask == idTask);
        this.tasks.splice(index, 1);
        this.updateLocalStorage(); 
        alert('Task deleted successfully');
    },
    markAsDone(idTask) {
        let index = this.tasks.findIndex(task => task.idTask == idTask);
        const taskToMove = this.tasks[index];

        this.tasks.splice(index, 1); // remove the task from the "To Do" list
        taskToMove.completed = true; // mark the task as completed
        this.tasks.push(taskToMove); // add the task to the "Done" list
        this.updateLocalStorage(); // update local storage after moving the task
        alert('Task marked as done.');
    },
    updateLocalStorage() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    getStoredTasks() {
            const storedTasks = localStorage.getItem('tasks');
            return storedTasks ? JSON.parse(storedTasks) : [];
    },
  },
  mounted() {
    const storedTasks = localStorage.getItem('tasks');
    if (storedTasks) {
        this.tasks = JSON.parse(storedTasks);
    }
  },
};
</script>


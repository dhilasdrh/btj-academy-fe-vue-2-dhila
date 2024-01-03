<template>
  <div class="py-5 px-8 bg-slate-100 mx-4 my-5 rounded-lg">
    <h3 class="text-2xl text-gray-800 font-medium">Add New Task</h3>

    <Message
      v-if="errorMessage || successMessage"
      :visible="errorMessage || successMessage"
      :title="errorMessage ? 'Error!' : 'Success!'"
      :message="errorMessage ? 'Task name must not be empty.' : 'Task successfully added.'"
      :borderColor="errorMessage ? 'border-red-700' : 'border-green-800'"
      :backgroundColor="errorMessage ? 'red-200' : 'green-200'" 
      :textColor="errorMessage ? 'text-red-800' : 'text-green-800'"
    />

    <form @submit.prevent="addNewTask" class="flex flex-col md:flex-row my-4 gap-3 justify-center">     
      <div class="basis-2/5 w-full">
        <label for="taskName" class="block mb-2 font-medium text-gray-800 dark:text-white">Name</label>
        <input v-model="newTask.name" type="text" id="taskName" placeholder="Enter new task name here" class="w-full bg-gray-50 form-input border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required>
      </div>

      <div class="basis-2/5 w-full">
        <label for="taskPriority" class="block mb-2 font-medium text-gray-800 dark:text-white">Priority</label>
        <select v-model="newTask.priority" id="taskPriority" class="w-full bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
          <option selected value="Low">Low</option>
          <option value="Medium">Medium</option>
          <option value="High">High</option>
        </select>
      </div>

      <div class="flex basis-1/5 items-end">
        <button @click="addNewTask" class="w-full middle none center rounded-sm bg-blue-500 py-2 px-10 text-white shadow-md shadow-indigo-500/20 transition-all hover:shadow-lg hover:shadow-indigo-500/40 focus:opacity-[0.85] focus:shadow-none active:opacity-[0.85] active:shadow-none disabled:pointer-events-none disabled:opacity-50 disabled:shadow-none">
          Save
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import Message from './MessageDisplay.vue';

export default {
  components: {
    Message,
  },
  data() {
    return {
      newTask: {
        name: "",
        priority: "Low",
      },
      errorMessage: false,
      successMessage: false,
    };
  },
  methods: {
    addNewTask() {
      if (this.newTask.name.trim() === "") {
        this.errorMessage = true;
        setTimeout(() => {
          this.errorMessage = false;
        }, 3000);
      } else {
        this.$emit('new-task', {
          name: this.newTask.name,
          priority: this.newTask.priority,
          completed: false,
        });

        this.newTask.name = "";
        this.newTask.priority = "Low";
        this.successMessage = true;
        setTimeout(() => {
          this.successMessage = false;
        }, 3000);
      }
    },
  },
};
</script>
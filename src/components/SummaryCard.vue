<template>
  <div :class="[getPriorityColorClass(), 'basis-1/4 card py-3 text-center items-center rounded-lg']">
    <h4 class="text-slate-700 text-lg">{{ title }}</h4>
    <h1 class="text-6xl">{{ count }}</h1>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    count: Number,
  },
  methods: {
    getPriorityColorClass() {
      const priorityClasses = {
        'Pending': 'bg-green-400/50 text-green-700',
        'Low Priority': 'bg-blue-400/50 text-blue-700',
        'Medium Priority': 'bg-yellow-400/50 text-yellow-700',
        'High Priority': 'bg-red-400/50 text-red-700',
      };
      return priorityClasses[this.title] || 'bg-green-500/50 text-green-700';
    },
  },
};
</script>

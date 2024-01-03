<template>
  <div>
    <div class="container flex flex-col sm:flex-row py-5 px-4 gap-4">
      <SummaryCard title="Pending" :count="totalPendingTask" />
      <SummaryCard title="Low Priority" :count="totalLowPriorityTask" />
      <SummaryCard title="Medium Priority" :count="totalMediumPriorityTask" />
      <SummaryCard title="High Priority" :count="totalHighPriorityTask" />
    </div>
  </div>
</template>

<script>
import SummaryCard from './SummaryCard.vue';

export default {
  props: {
    totalPendingTask: Number,
    totalLowPriorityTask: Number,
    totalMediumPriorityTask: Number,
    totalHighPriorityTask: Number,
  },
  components: {
    SummaryCard,
  },
  mounted() {
    console.log('SummarySection is mounted');
  },
  watch: {
    totalPendingTask(newValue, oldValue) {
      console.log('totalPendingTask changed from', oldValue, 'to', newValue);
    },
  },
};
</script>
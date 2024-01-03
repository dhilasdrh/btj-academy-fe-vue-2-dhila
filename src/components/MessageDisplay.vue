<template>
  <div v-if="visible" :class="[`border ${borderColor} bg-${backgroundColor} mt-2 p-2`]">
    <p :class="textColor"><strong>{{ title }}</strong> {{ message }}</p>
  </div>
</template>

<script>
export default {
  props: {
    visible: Boolean,
    title: String,
    message: String,
    borderColor: String,
    backgroundColor: String,
    textColor: String,
  },
  created() {
    console.log('MessageDisplay props:', this.$props);
  },
};

</script>

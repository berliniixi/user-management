<script setup>
const props = defineProps({
  location: {
    type: Object,
  },
});
</script>

<template>
  <div class="body-info_container">
    {{ props.location }}
    <div></div>
  </div>
</template>


<style scoped>

</style>
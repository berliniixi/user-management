<script setup>
const props = defineProps({
  title: {
    type: String,
    default: "",
  },
  subtitle: {
    type: String,
    default: "",
  },
});
</script>

<template>
  <div class="custom-header_container">
    <h1>{{ props.title }}</h1>
    <h4>{{ props.subtitle }}</h4>
  </div>
</template>

<style scoped>
.custom-header_container {
  display: flex;
  width: 100%;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  background-color: rgb(70, 144, 70);
  padding-bottom: 1rem;
}
</style>

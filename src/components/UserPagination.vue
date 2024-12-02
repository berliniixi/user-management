<script setup>
const props = defineProps({
  countries: {
    type: [],
  },
  nat: {
    type: String,
  },
});
</script>

<template>
  <div>
    <select v-model="props.nat">
      <option v-for="(country, index) in props.countries" :key="index">
        {{ country }}
      </option>
    </select>
  </div>
</template>

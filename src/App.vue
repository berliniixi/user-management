<script setup>
import CustomHeader from "./components/CustomHeader.vue";
import UserListing from "./components/UserListing.vue";
// import axios from "axios";
// import { onMounted } from "vue";

// onMounted(async () => {
//   const res = await axios.get("https://randomuser.me/api/?results=10");
// });
</script>

<template>
  <div class="app_container">
    <custom-header
      title="User Management App"
      subtitle="Find all available user information "
    />
    <div class="app_user-listing"></div>
    <user-listing />
  </div>
</template>

<style scoped>
.app_user-listing {
  display: flex;
  flex-wrap: wrap;
}
</style>

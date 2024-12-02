<script setup>
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import UserCard from "./UserCard.vue";
import UserModal from "./UserModal.vue";

import HeaderInfo from "./InfoCard/HederInfo.vue";
import BodyInfo from "./InfoCard/BodyInfo.vue";

import axios from "axios";
import { onMounted, ref } from "vue";

const users = ref([]);
const isLoading = ref(false);
const err = ref("");
const isUserClicked = ref(false);
const clickedUser = ref({});

onMounted(async () => {
  try {
    isLoading.value = true;
    const res = await axios.get("https://randomuser.me/api/?results=10");
    users.value = await res.data.results;
  } catch (error) {
    err.value = error.message;
  } finally {
    isLoading.value = false;
  }
});

const handleOnUserClicked = (user) => {
  isUserClicked.value = true;
  clickedUser.value = user;
};
</script>

<template>
  <user-modal :isOpen="isUserClicked">
    <template #header>
      <header-info
        :fullname="clickedUser.name"
        :picture="clickedUser.picture.large"
        :email="clickedUser.email"
        :phone="clickedUser.phone"
        :gender="clickedUser.gender"
      />
    </template>
    <template #content>
      <body-info :location="clickedUser.location" />
    </template>
    <template #footer>
      <div class="modal-footer">
        <button @click="isUserClicked = false">Close</button>
      </div>
    </template>
  </user-modal>
  <div class="user-listing_container">
    <div v-if="isLoading" class="user-listing_loader">
      <pulse-loader :loading="isLoading" />
    </div>

    <div v-if="err" class="error">{{ err }}</div>

    <div v-if="!isLoading" class="user-listing_user_card">
      <user-card
        v-for="(user, index) in users"
        :key="index"
        :user="user"
        @onUserClick="(user) => handleOnUserClicked(user)"
      />
    </div>
  </div>
</template>

<style scoped>
.user-listing_container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding-top: 3rem;
  height: 70vh;
}

.user-listing_loader {
  display: flex;
  justify-content: center;
  width: 100%;
  height: 100vh;
  align-items: center;
}

.user-listing_user_card {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
}

.error {
  color: red;
  font-size: 1.2em;
}

.modal-footer {
  display: flex;
  width: 100%;
  height: 25vh;
  justify-content: end;
  align-items: end;
}

.modal-footer button {
  width: 200px;
  height: 40px;
  border-radius: 0.7rem;
  border: 2px solid rgb(70, 144, 70);
  background-color: transparent;
}

.modal-footer button:hover {
  transition: 0.3s;
  background-color: rgb(70, 144, 70);
  cursor: pointer;
}
</style>

<script setup>
import { computed } from "vue";

const props = defineProps({
  user: { type: Object, default: {} },
});
const emit = defineEmits({
  onUserClick: { user: Object },
});

const userImg = computed(() => props.user.picture.medium);

const fullname = computed(
  () =>
    `${props.user.name.title} ${props.user.name.first} ${props.user.name.last}`
);

const formatDate = (date) => {
  return date.split("T")[0];
};

const dateOfBirth = computed(() => formatDate(props.user.dob.date));
const nationality = computed(() => props.user.nat);
</script>

<template>
  <div class="user-card_container" @click="emit('onUserClick', props.user)">
    <div class="user-card_img">
      <img :src="userImg" :alt="fullname" />
    </div>
    <div class="user-card_info">
      <h3>{{ fullname }}</h3>
      <h5>{{ dateOfBirth }}</h5>
      <h4>{{ nationality }}</h4>
    </div>
  </div>
</template>

<style scoped>
.user-card_container {
  display: flex;
  width: 35%;
  flex-direction: row;
  align-items: center;
  gap: 1.5rem;
  padding: 1rem;
}

.user-card_container:hover {
  cursor: pointer;
  border-radius: 1rem;
  background-color: rgb(232, 232, 232);
}

.user-card_img img {
  border-radius: 100%;
}

.user-card_info {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.user-card_info h5 {
  color: gray;
}
</style>

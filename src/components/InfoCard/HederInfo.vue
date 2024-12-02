<script setup>
import { computed } from "vue";
const props = defineProps({
  fullname: {
    type: Object,
  },
  phone: {
    type: String,
  },
  email: {
    type: String,
  },
  gender: {
    type: String,
  },
  picture: {
    type: String,
    default: "https://placehold.co/120x120",
  },
});

const genderIcon = computed(() =>
  props.gender === "male" ? "fa fa-mars" : "fa fa-venus"
);

const genderColor = computed(() => (props.gender === "male" ? "blue" : "pink"));

const username = computed(
  () => `${props.fullname.title} ${props.fullname.first} ${props.fullname.last}`
);
</script>

<template>
  <div class="header-info_container">
    <div class="header-info_img_container">
      <div class="image">
        <img :src="props.picture" />
      </div>
    </div>
    <div class="fullname">
      <i :class="genderIcon" :style="{ color: genderColor }"></i>
      <h3>{{ username }}</h3>
    </div>
    <div class="personal-info">
      <span>
        <p>{{ props.email }}</p>
        <p>{{ props.phone }}</p>
      </span>
    </div>
  </div>
</template>

<style scoped>
.header-info_container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  justify-content: center;
  margin: 3rem;
}

.background {
  z-index: 2;
  width: 100%;
  background-color: red;
}

.image img {
  border-radius: 100%;
}

.fullname {
  display: flex;
  justify-content: center;
  flex-direction: row;
  gap: 1rem;
}

.personal-info span {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 1rem;
}
</style>

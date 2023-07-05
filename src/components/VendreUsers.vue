<script setup>

import { ref, onMounted } from 'vue';

defineProps({
  msg: {
    type: String,
    required: true
  }
});

const users = ref([]);

onMounted(async () => {
  try {
    const response = await fetch('https://reqres.in/api/users');
    const data = await response.json();
    users.value = data.data.map(user => ({
      ...user,
      avatar: user.avatar
    }));
  } catch (error) {
    console.error(error);
  }
});
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3 v-if="users.length > 0">
      You’ve successfully created a project with
      <a href="https://vitejs.dev/" target="_blank" rel="noopener">Vite</a> +
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>.
    </h3>
    <ul v-if="users.length > 0">
      <li v-for="user in users" :key="user.id">
        <img :src="user.avatar" :alt="'avatar ' + user.id">
        {{ user.first_name }} {{ user.last_name }} {{ user.email }}
      </li>
    </ul>
    <p v-else>Loading...</p>
  </div>
</template>


<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>

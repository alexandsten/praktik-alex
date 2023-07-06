<script setup>
import { ref, onMounted, defineProps } from 'vue';

const props = defineProps(['api'])

const users = ref([]);

onMounted(async () => {
  try {
    const response = await fetch(props.api);
    console.log(props.api)
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
  <div class="userList">
    <ul v-if="users.length > 0" class="userList__row">
      <li v-for="user in users" :key="user.id" class="userList__item">
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

.userList {
  width: 100vw; 
  height: 100vh; 
  display: flex;
  align-items: center;
  justify-content: center;
}

.userList__row {
  display: flex;
  flex-wrap: wrap; 
  justify-content: center;
  align-content: center;
}

.userList__item {
  flex: 0 0 calc(33.33% - 10px); 
  margin-bottom: 20px; 
}

@media (max-width: 1024px) {
  .userList__item {
    flex: 0 0 calc(50% - 10px); 
  }
  
  .userList h1,
  .userList h3 {
    text-align: left;
  }
}
</style>
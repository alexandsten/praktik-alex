<script setup>
import { ref, onMounted } from 'vue';

const props = defineProps(['api'])  // API för sida 1 eller 2, sänds från App.vue

const users = ref([]);  // Variabel som bär på info om Vendre Anställda, hämtas från API

onMounted(async () => {   // API anrop
  try {
    const response = await fetch(props.api);
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
        <img :src="user.avatar" :alt="'avatar ' + user.id" class="vendreAvatar">
        <div> 
          <p>{{ user.first_name }} {{ user.last_name }}</p>
        </div>
          <a :href="`mailto:${user.email}`">Contact</a>
      </li>
    </ul>
    <p v-else>Laddar</p>
  </div>
</template>


<style scoped>
.userList {
  font-family: sans-serif;
  width: 100%;
  height: 90vh; 
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: row; 
  margin-top: 25px;
  padding-top: 45px;
}

.userList__row {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-content: center;
  margin-top: 20px; 
}

.userList__item {
  width: 170px;
  margin: 10px;
  display: flex; 
  flex-direction: column; 
  justify-content: center; 
  align-items: center; 
  background-color: rgb(218, 216, 216);
  border-radius: 5px;
  padding: 8px;
  box-shadow: 3px 3px  rgb(167, 167, 167);
}

.vendreAvatar {
  border-radius: 50%;
  margin: 12px 0px;
}

@media (max-width: 720px) {
  .userList {
      padding-top: 75px;
  }
}

@media (max-width: 450px) {
  .userList {
      padding-top: 130%;
  }
}
</style>
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
        <div> 
          {{ user.first_name }} {{ user.last_name }}
        </div>
        <div> {{ user.email }}</div>
      </li>
    </ul>
   
    <p v-else>Loading...</p>
  </div>
</template>


<style scoped>
.userList {
  width: 100%;
  height: 90vh; /* Make userList cover the entire viewport height */
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: row; /* Center the content vertically */
}

/* Adjust the width and height of userList__row and userList__item as needed */
.userList__row {
  width: 90%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-content: center;
  margin-top: 20px; /* Add margin between userList__row and userList */
}

.userList__item {
  flex: 0 0 calc(16%); /* Adjust the width and margin as needed */
  margin: 4px;
}

/* Add media queries to adjust the layout for smaller screens */
@media (max-width: 1024px) {
  .userList__item {
    flex: 0 0 calc(20%);
  }

  .userList h1,
  .userList h3 {
    text-align: left;
  }
}
</style>
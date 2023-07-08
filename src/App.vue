<template>
  <main>
    <div class="users">
      <img src="src\assets\vendre.png" alt="logo" width="155" height="55">
      <button @click="startVendreUsers">Page 1</button>
      <button @click="startVendreUsers2">Page 2</button>
    </div>
      <component v-if="showVendreUsers" :is="VendreUsers" api="https://reqres.in/api/users" />
      <component v-if="showVendreUsers2" :is="VendreUsers" api="https://reqres.in/api/users?page=2" />
  </main>
</template>

<script setup>
import { ref } from 'vue';

import VendreUsers from './components/VendreUsers.vue';

// Pages boolean, page 1 ska visas när sidan öppnas
const showVendreUsers = ref(true);
const showVendreUsers2 = ref(false);

// Respektive knapp ska visa sin page och dölja den andre när den klickas på
const startVendreUsers = () => {
  showVendreUsers2.value = false;
  showVendreUsers.value = true;
};

const startVendreUsers2 = () => {
  showVendreUsers.value = false;
  showVendreUsers2.value = true;
};
</script>


<style scoped>

main {
    background-color: rgb(248, 246, 237);
}

.users {
  display: flex; 
  justify-content: end; 
  align-items: center; 
  margin-right: 7%;
}

.users img {
  margin-right: 20%;
}

.users button {
  font-family: sans-serif;
  width: 120px;
  height: 30px;
  background-color: rgb(244, 244, 244);
  border: 3px solid rgb(219, 219, 219);
  border-radius: 15px;
  box-shadow: 3px 3px  rgb(141, 141, 141);
  margin: 3px;
}

.users button:hover {
  color: white;
  background-color: rgb(65, 65, 65);
  border: 3px solid rgb(241, 240, 240);
}

@media (max-width: 640px) {
  .users button {
  width: 100px;
  height: 25px;
  }
}
</style>

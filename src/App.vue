<template>

  <main>
    <div class="users">
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


.users {
  display: flex; 
  justify-content: end; 
  align-items: center; 
  margin-right: 7%;
}

.users button {
  width: 120px;
  height: 30px;
}


@media (max-width: 640px) {
  .users button {
  width: 80px;
  height: 20px;
}
}
</style>

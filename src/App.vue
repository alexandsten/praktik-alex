<template>

  <main>
    <component v-if="showVendreUsers" :is="VendreUsers" api="https://reqres.in/api/users" />
    <component v-if="showVendreUsers2" :is="VendreUsers" api="https://reqres.in/api/users?page=2" />
    <div class="wrapper">
      <button @click="startVendreUsers">Page 1</button>
      <button @click="startVendreUsers2">Page 2</button>
    </div>
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
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>

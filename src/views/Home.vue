<template>
  <div>
    <h2>Home HOme HOMe HOME</h2>
    <p v-if="loggedInUser">
      WELCOME <b>{{ loggedInUser }}</b
      >!
    </p>
    <p v-else>로그인이 필요해요😂</p>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";

const loggedInUser = ref(null);
onMounted(() => {
  loggedInUser.value = localStorage.getItem("loggedInUser");
});
</script>

<style scoped></style>

<template>
  <div>
    <h2>LoGIn</h2>
    <form @submit.prevent="login">
      <input v-model="username" type="text" placeholder="아이디 입력" />
      <input v-model="password" type="password" placeholder="비밀번호 입력" />
      <button type="submit">로그인</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();

const username = ref("");
const password = ref("");
const login = () => {
  const saved = localStorage.getItem("user");
  if (!saved) {
    alert("저장된 정보가 없어요! 회원가입이 필요해요😣");
    router.push("/signup");
    return;
  }
  const user = JSON.parse(saved);
  if (username.value === user.username && password.value === user.password) {
    alert("로그인 성공😎");
    // 로그인 성공했을 때 저장용 (로그인 / 로그아웃 제어)
    localStorage.setItem("loggedInUser", username.value);
    router.push("/");
  } else {
    alert("아이디나 비밀번호가 불일치🥴");
  }
};
</script>

<style scoped></style>

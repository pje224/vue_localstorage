<template>
  <div>
    <router-link to="/">Logo</router-link>│ <router-link to="/reserve">예약하기</router-link>│
    <router-link to="/confirm">예약확인</router-link>│ <router-link to="/review">리뷰</router-link>│
    <!-- 로그인 상태에 따라 메뉴 변경 -->
    <span v-if="loggedInUser">{{ loggedInUser }}님 <button @click="logout">로그아웃</button></span>
    <!-- 기본 메뉴 -->
    <span v-else>
      <router-link to="/login">로그인</router-link>│
      <router-link to="/signup">회원가입</router-link>
    </span>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";

const loggedInUser = ref(null);
// 로그인 상태 체크
const checkLogin = () => {
  const user = localStorage.getItem("loggedInUser");
  loggedInUser.value = user ? user : null;
};
// 페이지가 열릴 때 한 번 실행
onMounted(() => {
  checkLogin();
});
// 로그아웃
const logout = () => {
  localStorage.removeItem("loggedInUser");
  alert("로그아웃 됐어요😢");
};
</script>

<style scoped></style>

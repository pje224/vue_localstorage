<template>
  <div>
    <router-link to="/">Logo</router-link>│ <router-link to="/reserve">예약하기</router-link>│
    <router-link to="/confirm">예약확인</router-link>│ <router-link to="/review">리뷰</router-link>│
    <!-- 로그인 상태에 따라 메뉴 변경 -->
    <span v-if="loggedInUser">{{ loggedInUser }}님 <button @click="logout">로그아웃</button></span>
    <!-- 기본 메뉴 -->
    <span v-else>
      <router-link to="/login">로그인</router-link>│
      <router-link to="/signup">회원가입</router-link> </span
    >│
    <!-- 다크 모드 버튼 -->
    <button class="theme-btn" @click="toggleTheme">
      {{ isDark ? "🌙 다크 모드" : "☀️ 라이트 모드" }}
    </button>
  </div>
</template>

<script setup>
import { onMounted, ref, watch } from "vue";

// 다크 모드 설정
const isDark = ref(false);
const THEME_KEY = "theme";

const loggedInUser = ref(null);
// 로그인 상태 체크
const checkLogin = () => {
  const user = localStorage.getItem("loggedInUser");
  loggedInUser.value = user ? user : null;
};
// 페이지가 열릴 때 한 번 실행
onMounted(() => {
  checkLogin();
  // 다크 모드 설정
  // 로컬에서 테마 불러오기
  const savedTheme = localStorage.getItem("THEME_KEY");
  isDark.value = savedTheme === "dark";
});
// 다크 모드 적용
watch(
  isDark,
  (val) => {
    // console.log(val);
    const el = document.documentElement;
    // console.log(el);  // html 전체를 뜻함

    if (val) {
      el.classList.add("dark");
      localStorage.setItem(THEME_KEY, "dark");
    } else {
      el.classList.remove("dark");
      localStorage.setItem(THEME_KEY, "light");
    }
  },
  { immediate: true }
);
// 다크 모드 버튼 클릭
const toggleTheme = () => {
  isDark.value = !isDark.value;
};
// 로그아웃
const logout = () => {
  localStorage.removeItem("loggedInUser");
  alert("로그아웃 됐어요😢");
};
</script>

<style lang="scss" scoped>
button {
  border: none;
  padding: 5px 8px;
  border-radius: 8px;
  background-color: #0a66c2;
  color: #fff;
}
</style>

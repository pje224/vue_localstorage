<template>
  <div>
    <h2>cOnfIrm LIsT</h2>
    <p>회원 : {{ loggedInUser }}</p>
    <div v-if="myReservations.length > 0">
      <ul>
        <li v-for="item in myReservations" :key="item.id">
          {{ item.name }}│{{ item.date }}
          <span v-if="isPast(item.date)">완료 ✅</span>
          <span v-else>예약 중 ⏳</span>
          <button @click="cancelReservation(item.id)">취소 ❌</button>
        </li>
      </ul>
    </div>
    <div v-else>
      <p>예약 정보가 없어요❌</p>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();

const loggedInUser = ref(null);
const reservations = ref([]);

onMounted(() => {
  const user = localStorage.getItem("loggedInUser");
  if (!user) {
    alert("로그인 후 확인 가능😞");
    router.push("/login");
    return;
  } else {
    loggedInUser.value = user;
  }
  const saved = localStorage.getItem("reservations");
  reservations.value = saved ? JSON.parse(saved) : [];
});
// 로그인 회원 예약만 필터
const myReservations = computed(() => {
  return reservations.value.filter((r) => r.name === loggedInUser.value);
});
// 예약 날짜가 지났는지 확인
const isPast = (dateStr) => {
  //   console.log(dateStr);
  const today = new Date().toISOString().split("T")[0]; // YYYY-MM-DD
  return dateStr < today;
};
// 예약 취소하기
const cancelReservation = (id) => {
  // console.log(id);
  reservations.value = reservations.value.filter((item) => item.id !== id);
  // 필터링 된 값을 로컬스토리지에 업데이트
  localStorage.setItem("reservations", JSON.stringify(reservations.value));
  alert("예약이 취소됐어요🤔");
};
</script>

<style lang="scss" scoped>
button {
  margin: 0 5px;
  border: none;
  padding: 5px 8px;
  border-radius: 8px;
  background-color: #0a66c2;
  color: #fff;
}
</style>

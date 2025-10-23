<template>
  <div>
    <div class="box">
      <h2>rEvIeW</h2>
      <!-- 로그인 상태 안내 -->
      <p>회원 : {{}}</p>
      <p>리뷰 작성은 로그인 후 가능해요🤔</p>
      <!-- 리뷰 입력창 (로그인한 회원만 표시) -->
      <div class="form">
        <input type="number" min="1" max="5" placeholder="⭐" />
        <textarea placeholder="후기를 입력하세요"></textarea>
        <button>리뷰 저장하기</button>
      </div>
    </div>
  </div>
</template>

<script setup></script>

<stylescoped></stylescoped>

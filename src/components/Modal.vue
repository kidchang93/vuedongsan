<template>
  <!-- 모달창 -->
  <div class="black-bg" v-if="modal == true">
    <div class="white-bg">
      <img :src="oneRooms[userClick].image" class="room-img" />
      <h4>{{ oneRooms[userClick].title }}</h4>
      <p>{{ oneRooms[userClick].content }}</p>
      <!-- <input @input="month = $event.target.value" /> -->
      <!-- 축약 버전 -->
      <input v-model="month" />
      <!-- <textarea v-model="month"></textarea> -->
      <!-- <select v-model="month">
        <option value="123123">adfadsf</option>
      </select> -->
      <input type="range" min="1" max="12" />
      <p>{{ month }} 개월 선택함 : {{ oneRooms[userClick].price * month }}</p>

      <button @click="$emit('closeModal', false)">닫기</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "Modal",

  data() {
    return {
      // 데이터 쓸 수 있는데 웬만하면 최상위 컴포넌트에 데이터 만들어두고 props로 부르는게
      month: 1,
    };
  },
  props: {
    oneRooms: Array,
    userClick: Number,
    // 버튼에 있는 modal은 여기서 수정하면 안된다. 그래서 활성화시키면 에러뜬다.
    modal: Boolean,
  },
  methods: {
    // closeModal() {
    //  this.$emit("closeModal");
    // },
  },
  watch: {
    month(a) {
      if (isNaN(a) == true) {
        alert("문자 입력하지마셈");
        this.month = 1;
      }
    },
  },
  // input에 update (리렌더링) 전에 hook을 걸어서 alert띄우기
  beforeUpdate() {
    if (this.month == 2) {
      alert("최소2 이상 입력하세요");
      this.month = 1;
    }
  },
};
</script>
<style></style>

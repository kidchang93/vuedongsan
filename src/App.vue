<template>
  <!-- props활용 -->
  <Transition name="fade">
    <Modal
      :oneRooms="oneRooms"
      :userClick="userClick"
      :modal="modal"
      @closeModal="modal = $event"
    />
  </Transition>
  <!-- navbar -->

  <div class="menu">
    <a v-for="menu in menus" :key="menu">{{ menu }}</a>
  </div>

  <!-- banner -->
  <Discount v-if="showDiscount == true" :salePercent="salePercent" />
  <!-- <Card
    :oneRooms="oneRooms"
    :userClick="userClick"
    :modal="modal"
    :name="object.name"
    :age="object.age"
    v-bind="object"
  /> -->

  <!-- 상품 정렬 -->
  <button @click="priceSort">가격순 정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card
    @openModal="
      modal = true;
      userClick = $event;
    "
    :oneRooms="oneRooms[i]"
    v-for="(item, i) in oneRooms"
    :key="i"
  />
  <!-- emit 으로 넘어온 데이터는 @작명= 이렇게 하고 메시지와 데이터도 같이 보낼 수 있다.
  부모 컴포넌트는 $event -> 룸object.id를 보냈다 이거로 수신한다. 기존엔 i 로 했었음-->
  <!-- Card 에 오브젝트 자체를 보낼 수 있다. -->
</template>

<script>
import Modal from "./components/Modal.vue";
import Discount from "./components/Discount.vue";
import Card from "./components/Card.vue";

import data from "./data/data.js";

export default {
  name: "app",
  components: { Discount, Modal, Card },
  data() {
    return {
      orgOneRooms: [...data],
      object: { name: "lee", age: "20" },
      oneRooms: data,
      modal: false,
      price1: 60,
      price2: 70,
      menus: ["HOME", "PRODUCTS", "ABOUT"],
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
      counters: 0,
      userClick: 0,
      showDiscount: true,
      salePercent: 50,
    };
  },
  methods: {
    counter() {
      this.counters += 1;
    },
    priceSort() {
      // sort 함수 = [3, 5, 2].sort()
      // 출력 : [2, 3, 5] -> 문자 정렬
      // var array = [3, 5, 2];
      // a , b = 데이터
      // 음수면 a 를 왼쪽으로 보내주세요 라는 로직을 갖고있다.
      // 원본을 변형
      this.oneRooms.sort((a, b) => {
        return a.price - b.price;
      });
    },
    sortBack() {
      // 되돌리기
      // 등호를 쓴 array 는 공유해주세요 라는 뜻
      // 그래서 스프레드 연산자 또 써줘야함
      this.oneRooms = [...this.orgOneRooms];
    },
  },
  // 서버에서 데이터 가져올때 lifeCycle hook 안에 코드 짬
  created() {
    // 서버에서 데이터 가져오는 중
  },
  mounted() {
    // setTimeout(() => {
    //   this.showDiscount = false;
    // }, 2000);
    setInterval(() => {
      // 1초마다 1퍼씩 감소하는 로직
      this.salePercent -= 1;
    }, 1000);
  },

  beforeMount() {},
};
</script>

<style>
.start {
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
}
/* 모달 닫힐 때 */
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}
/* 모달 열릴 때 */
.fade-enter-from {
  transform: translateY(-1000px);
  /* opacity: 0; */
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  transform: translateY(0px);
  /* opacity: 1; */
}
body {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  position: fixed;
  padding: 20px;
}
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
</style>

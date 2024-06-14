<template>
  <!-- 모달창 -->
  <div class="black-bg" v-if="modal == true">
    <div class="white-bg">
      <img :src="oneRooms[userClick].image" class="room-img" />
      <h4>{{ oneRooms[userClick].title }}</h4>
      <p>{{ oneRooms[userClick].content }}</p>
      <p>{{ oneRooms[userClick].price }}</p>

      <button @click="modal = false">닫기</button>
    </div>
  </div>
  <!-- banner -->
  <Discount />

  <!-- navbar -->
  <div class="menu">
    <a v-for="menu in menus" :key="menu">{{ menu }}</a>
  </div>
  <!-- main -->
  <div v-for="(item, i) in oneRooms" :key="i">
    <img :src="oneRooms[i].image" class="room-img" />
    <h4
      @click="
        modal = true;
        userClick = i;
      "
    >
      {{ oneRooms[i].title }}
    </h4>
    <p>{{ oneRooms[i].price }}원</p>
    <!-- <button @click="counters[i]++">허위매물 신고</button>
    <span>신고 수 : {{ counters[i] }}</span> -->
  </div>
</template>

<script>
import Discount from "./components/Discount.vue";
import data from "./data/data.js";

export default {
  name: "app",
  components: { Discount },
  data() {
    return {
      oneRooms: data,
      modal: false,
      price1: 60,
      price2: 70,
      menus: ["HOME", "PRODUCTS", "ABOUT"],
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
      counters: 0,
      userClick: 0,
    };
  },
  methods: {
    counter() {
      this.counters += 1;
    },
  },
};
</script>

<style>
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

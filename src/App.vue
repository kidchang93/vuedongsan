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
  <Discount />
  <!-- <Card
    :oneRooms="oneRooms"
    :userClick="userClick"
    :modal="modal"
    :name="object.name"
    :age="object.age"
    v-bind="object"
  /> -->
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
      object: { name: "lee", age: "20" },
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
.start {
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
}

.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  opacity: 1;
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

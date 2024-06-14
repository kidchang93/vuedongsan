<template>
  <!-- main -->
  <div>
    <img :src="oneRooms.image" class="room-img" />
    <!-- <h4
      @click="
        $emit.modal = true;
        userClick = i;
      "
    >
      {{ oneRooms[i].title }}
    </h4> -->

    <h4 @click="openModal">{{ oneRooms.title }}</h4>

    <p>{{ oneRooms.price }}원</p>

    <!-- <button @click="counters[i]++">허위매물 신고</button>
    <span>신고 수 : {{ counters[i] }}</span> -->
  </div>
</template>
<script>
export default {
  name: "Card",
  data() {
    return {};
  },
  props: {
    oneRooms: Object,
    userClick: Number,
    modal: Boolean,
  },
  methods: {
    openModal() {
      this.$emit("openModal", this.oneRooms.id);
    },
  },
};
</script>
<style></style>

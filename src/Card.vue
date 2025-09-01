<template>
<!-- 매물 반복해서 표시 -->
  <div>
    <img :src="건수.image" class="room-img">
    <!-- <h4 @click="모달창열렸니 = true; 누른거 = i">{{ 건수.title }}</h4> -->
    <!-- <h4 @click="$emit('openModal', 건수.id)">{{ 건수.title }}</h4>   1) 부모에게 메시지 보낼 때, $emit('작명', 데이터) -->
    <h4 @click="send">{{ 건수.title }}</h4>   <!-- 2) 함수 아래에 정의하여 호출하기 -->
    <p>{{ 건수.price }} 원</p>
  </div>
</template>

<script>
  export default {
    name: 'Card',
    props : {
      건수 : Object,
    },
    methods: {
      send() {
        this.$emit('openModal', this.건수.id)
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>
<template>
  <div class="menu">
    <a v-for="title in titles" :key="title">{{ title }}</a>   <!-- vue HTML 반복문 <태그 v-for="작명 in n회"> -->
    <!-- <hr> -->
    <!-- <a v-for="(title,i) in titles" :key="title">{{ i }}</a>    vue HTML 반복문 특) 변수 작명 2개까지 가능 (왼쪽변수는 array 내의 데이터 : 오른쪽변수는 1씩 증가하는 정수) -->
    <!-- <a>Products</a>
    <a>About</a> -->
  </div>

  <!-- 할인 배너 -->
  <!-- <div class="discount">
    <h4>지금 결제하면 20% 할인</h4>
  </div> -->
  <Discount/>
  
  <!-- 모달  -->
  <!-- <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <Discount/>
      <img :src="원룸들[누른거].image" style="width:100%">
      <h4>{{원룸들[누른거].title}}</h4>
      <p>{{원룸들[누른거].content}}</p>
      <p>{{ 원룸들[누른거].price }} 원</p>
      <button @click="모달창열렸니 = false">닫기</button>
    </div>
  </div> -->
  <Modal v-bind:원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니"></Modal>    <!--  :데이터이름="데이터이름"    부모 App.vue  -> 자식 Modal.vue 에게 props로 데이터 보내기 -->

  <!-- if문 -->
<!--   
  <div v-if="1 == 1">안녕하세요</div>
  <div v-else-if=" 1 == 2">안녕하세요2</div>
  <div v-else>안녕하세요3</div>
-->



<!-- 매물 반복해서 표시 -->
 
<!-- <div v-for="(건수, i) in 원룸들" :key="i"> -->
  <!-- <img :src="원룸들[i].image" class="room-img">
  <h4 @click="모달창열렸니 = true">{{ 원룸들[i].title }}</h4>
  <p>{{ 원룸들[i].price }} 원</p> -->
  <!-- <img :src="건수.image" class="room-img">
  <h4 @click="모달창열렸니 = true; 누른거 = i">{{ 건수.title }}</h4>
  <p>{{ 건수.price }} 원</p> -->
<!-- </div> -->

<!--  <Card @click="모달창열렸니 = true" :건수="원룸들[i]" v-for="(작명,i) in 원룸들" :key="작명"></Card> -->  <!-- 이벤트 버블링 현상으로 @click 이벤트 동작됨!-->
  <Card @openModal="모달창열렸니 = true; 누른거 = $event" 
  :건수="원룸들[i]" v-for="(작명,i) in 원룸들" :key="작명"></Card>  <!-- 자식이 보내 데이터는 $event 변수에 담겨있음  - 커스텀 이벤트  -->
  <!-- <Card :건수="원룸들[1]"></Card>
  <Card :건수="원룸들[2]"></Card>
  <Card :건수="원룸들[3]"></Card>
  <Card :건수="원룸들[4]"></Card>
  <Card :건수="원룸들[5]"></Card> -->
  
  <div>
    <!-- <img src="./assets/images/room0.jpg" class="room-img"> --> 
<!-- <img :src="원룸들[0].image" class="room-img"> -->
    <!-- <h4 v-for="(a,i) in products" :key="i">{{ products[i] }}</h4> -->
    <!-- <h4 class="red" :style="스타일">XX 원룸</h4>      HTML 속성도 데이터바인딩 가능!   :속성 = "데이터이름" -->
    <!-- <h4 @click="모달창열렸니 = true">{{ products[0] }}</h4> -->
<!-- <h4 @click="모달창열렸니 = true">{{ 원룸들[0].title }}</h4> -->
<!-- <p>{{ price1 }} 만원</p> <p>{{ 원룸들[0].price }} 원</p> -->

    <!-- <p v-for="price in prices" :key="prices">{{ price }}</p> -->
    <!-- <button v-on:click="신고수++">허위매물신고</button> <span>신고수 : {{ 신고수 }}</span>
    <button v-on:click="increase">허위매물신고</button> <span>신고수 : {{ 신고수 }}</span> -->
<!-- <button v-on:click="신고수[0]++">허위매물신고</button> -->
<!-- <span>신고수 : {{ 신고수[0] }}</span> -->
    <!-- <button @mouseover="신고수++">허위매물신고</button> <span>신고수 : {{ 신고수 }}</span> -->
  </div>

  <div>
    <!-- <h4>XX 원룸</h4> -->
    <!-- <img src="./assets/images/room1.jpg" class="room-img">
    <h4>{{ products[1] }}</h4>
    <p>{{ price2 }} 만원</p>
    <button @click="신고수[1]++">허위매물신고</button>
    <span>신고수 : {{ 신고수[1] }}</span> -->
  </div>
  <div>
    <!-- <h4>XX 원룸</h4> -->
    <!-- <img src="./assets/images/room2.jpg" class="room-img">
    <h4>{{ products[2] }}</h4>
    <p>{{ price3 }} 만원</p>
    <button @click="신고수[2]++">허위매물신고</button>
    <span>신고수 : {{ 신고수[2] }}</span> -->
  </div>

</template>

<script>
// import apple from './assets/oneroom.js';
// import {apple, apple2} from './assets/oneroom.js';
// apple
// apple2
import 작명 from './assets/oneroom.js';
import Discount from './DiscountBanner.vue';
import Modal from './Modal.vue';
import Card from './Card.vue'

export default {
  name : 'App',
  data() {  // state :  상태저장        -->> Modal.vue 공통컴포넌트 만들었지만 아래 데이터는?? --> props !
    return {
      price1 : 60, // object 자료형으로 데이터를 저장함. {자료이름:자료내용}
      price2 : 70,
      price3 : 45,
      스타일 : 'color : blue',
      products : ['역삼동원룸', '서초동원룸', '강동구원룸'],
      // products : 
      // prices : [60, 70, 45],
      titles : ['Home', 'Shop', 'About'],
      // 신고수 : 0,
      신고수 : [0, 0, 0],
      모달창열렸니 : false,
      원룸들 : 작명,
      누른거 : 0,
    }
  },
  methods : { // 함수 정의하는 곳
    increase() {
      this.신고수 += 1;
    },
    increases() {
      this.tl
    },
  },

  components : {
    Discount,  // 좌우 이름이 동일한 경우 하나로만 써도 됨. Discount : Discount,   ===>   Discount,
    Modal,
    Card,
  }
}
</script>

<style>
body {
  margin : 0;
}
div {
  box-sizing: border-box;
}
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
.black-bg {
  width: 100%; height:100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background : darkslateblue;
  padding : 15px;
  border-radius : 5px;
}
.menu a {
  color : white;
  padding : 10px;
}

.room-img {
  width : 100%;
  margin-top: 40px;
}
</style> 
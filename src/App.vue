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
  <Discount v-if="showDiscount == true" /> <!-- state(데이터) 만들기 -->

  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">되돌리기</button>

  
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

  <!-- vue에서 매끈한 UI 애니메이션 주는 법(1) -->
  <!-- <div class="start end"> -->
  <!-- <div class="start" :class="{end : 모달창열렸니}"> class명을 조건부로 넣으려면 {클래스명 : 조건 }   //조건이 true가 되면 클래스명 적용됨 -->
    <!-- <Modal @closeModal="모달창열렸니 = false" v-bind:원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니"></Modal>     :데이터이름="데이터이름"    부모 App.vue  -> 자식 Modal.vue 에게 props로 데이터 보내기 -->
  <!-- </div> -->

    <!-- vue에서 매끈한 UI 애니메이션 주는 법(2) -->
    <transition name="fade">
        <Modal @closeModal="모달창열렸니 = false" v-bind:원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니"></Modal>    <!--  :데이터이름="데이터이름"    부모 App.vue  -> 자식 Modal.vue 에게 props로 데이터 보내기 -->
    </transition>

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
  
<!-- @openModal="..." 이렇게 쓰는 건 사용자 정의 이벤트(custom event)임.
 즉, click이나 input 같은 브라우저 기본 이벤트가 아니라, 개발자가 자식 컴포넌트(Card.vue) 안에서 $emit('openModal')로 직접 만든 이벤트임. -->
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
      원룸들 : 작명,        // <<-- 정렬할 때 사용
      누른거 : 0,
      //원룸들오리지널 : 작명, (x)   // <<-- 원본 필요할 때 사용
      원룸들오리지널 : [...작명],  // (o)  array/object 데이터의 각각 별개의 사본을 만들려면 [...array자료]
      showDiscount : true,
    }
  },
  methods : { // 함수 정의하는 곳
    increase() {
      this.신고수 += 1;
    },
    increases() {
      this.tl
    },
    priceSort() {
      this.원룸들.sort(function(a,b){
        //return a - b  // object - object 빼기 (x)
        return a.price - b.price // oneroom.js 확인해보기
      });
      
      // var array = [3,5,2];   
      // //array.sort(); // 엄밀히 따지면, 안에 숫자가 아닌, 가나다 순 정렬중임.
      // array.sort(function(a,b){
      //   return a - b  // 이 줄을 실행했을 때, 음수면 a를 왼쪽으로, 양수면 오른쪽으로
      // });
      // console.log(array);
    },
    sortBack() {
      // [참고] sort()는 원본을 변형함   VS.   map() filter() 등은 원본을 보존함!  
      // this.원룸들 = this.원룸들오리지널;  <-- array를 등호로 집어넣는것이 아니고, 왼쪽 오른쪽 값을 공유하라는 의미임.. 따라서 아래코드처럼 해야함!! (주의)
      this.원룸들 = [...this.원룸들오리지널];
    }
  },
  created() {
    // 서버에서 데이터 가져오는 코드를 작성
  },
  // mounted() { // lifecycle hook
  //   setTimeout(() => {
  //     this.showDiscount = false;
  //   }, 2000);
  // },
  // mounted() { // mounted() -> 컴포넌트가 mount되고 나서 뭔가 실행시키고 싶을때 쓰는 함수
  // setInterval(() => {
  //   this.offPrice--;
  //   }, 1000); // 1초 마다 내부 코드 실행
  // },

  beforeMount() { // mount 전에 뭔가 실행하고 싶으면 여기에 기술

  },
  components : {
    Discount,  // 좌우 이름이 동일한 경우 하나로만 써도 됨. Discount : Discount,   ===>   Discount,
    Modal,
    Card,
  }
}
</script>

<style>
/* (모달)등장 애니메이션 */
.fade-enter-from {  /* .작명-enter-from {시작스타일}  */
  /* opacity: 0; */
  transform: translateY(-1000px);
}
.fade-enter-active {   /* .작명-enter-active {transition}  */
  transition: all 1s;
}
.fade-enter-to {    /* .작명-enter-to {끝날때 스타일}  */
  /* opacity: 1; */
  transform: translateY(0px);
}

/* (모달)퇴장 애니메이션 */
.fade-leave-from {  /* .작명-leave-from {시작스타일}  */
  opacity: 1;
}
.fade-leave-active {   /* .작명-leave-active {transition}  */
  transition: all 1s;
}
.fade-leave-to {    /* .작명-leave-to {끝날때 스타일}  */
  opacity: 0;
}

.start {
  opacity: 0;  /* 투명도  */
  transition: all 1s;  /* 1초 동안 변화 */
}
.end {
  opacity: 1;
}

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
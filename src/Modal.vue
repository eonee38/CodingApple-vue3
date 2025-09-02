<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <Discount/>
      <img :src="원룸들[누른거].image" style="width:100%">
      <h4>{{원룸들[누른거].title}}</h4>
      <p>{{원룸들[누른거].content}}</p>
      <!-- <input type="text" @input="month = $event.target.value"> --> <input v-model.number="month"> <!-- 사용자가 입력한 값을 데이터(문자자료형)으로 저장 | v-model.number 로 기술할 시, 문자를 숫자로 저장함-->
      <p> {{ month }} 개월 선택함 : {{ 원룸들[누른거].price * month}} 원</p>
      <p> {{ month }} 개월 선택함 : {{ 원룸들[누른거].price + month}} 원</p>  <!-- 사용자가 입력한 값(문자=>숫자)을 기존(price) 값에 더하기 -->
      <!-- <button @click="모달창열렸니 = false">닫기</button> --> 
                                <!-- props (모달창열렸니)는 수정불가. read-only   -> 부모 데이터 수정하기 위해 custom event 써야함. -->
      <textarea v-model="month"></textarea>
      <select v-model="month">
        <option>1번 선택</option>
        <option>2번 선택</option>
        <option>3번 선택</option>
        <option>4번 선택</option>
      </select>
      <input type="checkbox" v-model="month"> <!-- 체크 시 true를 반환 VS. 체크해제 시 false 반환 -->
      <input type="range" min="1" max="12">

      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
  export default {
    name : 'Modal',
    data() {
      return {
        month : 1, // ''
        date : 123
      }
    },
    watch : { // watcher!! (데이터 감시 + 유효성검사) --> BUT, Vue전용 form validation 라이브러리 설치하면 wathcer 안쓰고 쉽게 유효성검사 기능 구현 가능.
      month(inputValue) {    // month(after_MonthData, before_MonthData) {  <-- 파라미터 2개까지 입력가능! (왼쪽: 변경후 month 데이터임 , 오른쪽 : 변경 전 month 데이터)
        if(inputValue > 12) {//입력한 month가 13이상이면
          alert('13이상 입력 불가')
        }else if(typeof inputValue === 'string'){ // 사용자가 month를 글자로 입력하면   | input 태그에서 <input v-model="month"> 인 경우 -> 입력값은 모두 문자열일테니, isNaN() 사용해야함. 
          alert('숫자만 입력하시게나');
          this.month = 1;
        }
      },
      // month(a){
      //   if(isNaN(a) == true){  // isNaN() 안에 숫자를 입력하면 false, 글자 입력 시 true
      //     alert('문자입력하지마시게');
      //     this.month = 1;
      //   }
      // },
      date() {

      }
    },
    props : {
      원룸들 : Array,
      누른거 : Number,
      모달창열렸니 : Boolean,
    },
    beforeUpdate() {
      if(this.month == 2) {
        alert('2개월은 거래 불가함. 3개월부터 입력하세요~');
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>

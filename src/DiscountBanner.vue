<template>
  <div class="discount">
    <!-- <h4>지금 결제하면 30% 할인</h4> -->
    <h4>지금 결제하면 {{ offPrice }} % 할인</h4>
  </div>
</template>

<script>
  export default {
    name : 'Discount',
    data() {
      return {
        offPrice : 30,
      }
    },
    mounted() {
      const intervalId = setInterval(() => {
      this.offPrice--;
      console.log("현재값 : ", this.offPrice);

      if (this.offPrice < 1) {
        clearInterval(intervalId);
      }
      }, 1000);
    },
    // methods: {
    //   clearInterval() {

    //   }
    // },
  }
</script>

<style lang="scss" scoped>

</style>
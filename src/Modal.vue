<template>

  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <h4>{{ 원룸들[누른거].title }}</h4>
      <p>{{ 원룸들[누른거].content }}</p>
      <input v-model="month">
      <p>{{ month }}개월 선택함 : {{ 원룸들[누른거].price * month }} 원</p>

      <button @click="$emit('closeModal')">닫기</button>
      <Discount/>
    </div>
  </div>

</template>

<script>

import Discount from './Discount.vue'

export default {
    name : 'Modal',
    data(){
        return {
            month : 1,
        }
    },
    watch : {
        month(a){
            if(a >= 13){
                alert('13이상 입력하지 마셈');
            } else if (isNaN(a) == true){
                alert('문자입력하지마라');
                this.month = 1;
            }
        },
    },
    props : {
        원룸들 : Array,
        누른거 : Number,
        모달창열렸니 : Boolean,
    },
    beforeUpdate(){
         if(this.month == 2){
            alert('3개월 이상부터 결제가 가능합니다.');
            this.month = '';
        }
    },
    components: {
        Discount,
    }
}
</script>

<style>

</style>
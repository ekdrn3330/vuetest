<template>



  <transition name="fade">
    <Modal @closeModal="모달창열렸니 = false;" :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니" />
  </transition>
  
  <div class="menu">
    <a href="#" v-for="i in 메뉴들" :key="i">{{ i }}</a>
  </div>

  <Discount v-if="showDiscount == true" :percent="percent" />

  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">되돌리기</button>
  <button @click="priceSortReverse">가격역순정렬</button>
  <button @click="alphabeticalOrder">가나다정렬</button>
  
  <Card @openModal="모달창열렸니 = true; 누른거 = $event;" :원룸="원룸들[a]" v-for="(i, a) in 원룸들" :key="i" />



</template>

<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data(){
    return {
      percent : 30,
      showDiscount : true,
      원룸들오리지널 : [...data],
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,
      신고수 : [0, 0, 0],
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸']
    }
  },
  methods: {
    increase(){
      this.신고수 += 1;
    },
    alphabeticalOrder(){
      this.원룸들.sort((a, b) => {
        return a.title < b.title ? -1 : a.title > b.title ? 1 : 0;
      })
    },
    priceSortReverse(){
      this.원룸들.sort(function(a, b){
        return b.price - a.price;
      });
    },
    sortBack(){
      this.원룸들 = [...this.원룸들오리지널];
    },
    priceSort(){
      this.원룸들.sort(function(a, b){
        return a.price - b.price;
      });
    }
  },
  mounted(){
    var percentStop = setInterval(() => {
      this.percent --;
      if(this.percent == 0) {
        clearInterval(percentStop);
      }
    },1000);
  },
  components: {
    Discount,
    Modal,
    Card
  }
}
</script>

<style>
.fade-leave-from {opacity:1;}
.fade-leave-active {transition:all .3s;}
.fade-leave-to {opacity:0;}

.fade-enter-from {transform:translateY(-1000px);}
.fade-enter-active {transition:all .3s;}
.fade-enter-to {transform:translateY(0);}

body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.discount {
  background:#eee;
  padding:10px;
  margin:10px;
  border-radius:5px;
}

.black-bg {
  width:100%; height:100%;
  background: rgba(0,0,0,.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width:100%; background:#fff;
  border-radius: 8px;
  padding:20px;
}

.room-img {
  width: 400px;
  margin-top: 40px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color:#fff;
  padding: 10px;
}
</style>

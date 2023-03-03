<template>

<!-- <div class="black-bg" v-if="모달창열렸니 == true">
  <div class="white-bg">
    <img :src="원룸들[누른거].image" style="width:100%">
    <h4>{{ 원룸들[누른거].title }}</h4>
    <p>{{ 원룸들[누른거].content }}</p>
    <p>{{ 원룸들[누른거].price }} 원</p>
    <button @click="모달창열렸니 = false">닫기</button>
  </div>
</div> -->
<transition name="fade">
<ModalVue @closeModal="모달창열렸니 = false" :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니" />
</transition>

<div class="menu">
  <a v-for="(작명,i) in 메뉴들" :key="i"> {{ 작명 }}</a>
</div>

<DiscountVue/>

<button @click="priceSort()">가격순 정렬</button>
<button @click="SortBack()">되돌리기</button>

<!-- <div v-for="(a, i) in 원룸들" :key="i">
  <img :src="a.image" class="room-img">
  <h4 @click="모달창열렸니 = true; 누른거 = i">{{a.title}}</h4>
  <p>{{a.price}}</p>
</div> -->

<CardVue @openModal="모달창열렸니 = true; 누른거 = $event" :원룸="원룸들[i]" v-for="(작명,i) in 원룸들" :key="작명" />

</template>

<script>

import roomdata from './assets/RoomData'
import CardVue from './components/Card.vue'
import DiscountVue from './components/Discount.vue'
import ModalVue from './components/Modal.vue'

export default {
  name: 'App',
  data(){
  return {
    누른거 : 0,
    원룸들원본 : [...roomdata],
    원룸들 : roomdata,
    메뉴들 : ['Home', 'Shop', 'About'],
    모달창열렸니 : false,
  }
},
methods : {
  SortBack(){
    this.원룸들 = [...this.원룸들원본];
  },
  priceSort(){
    this.원룸들.sort(function(a,b){
      return a.price - b.price
    })
  },
  },
  components: {
    roomdata,
    DiscountVue,
    ModalVue,
    CardVue,
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

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
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

.discount {
  background: #eee;
  padding:  10px;
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
.menu {
  background : darkslateblue;
  padding : 15px;
  border-radius : 5px;
}
.menu a {
  color : white;
  padding : 10px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

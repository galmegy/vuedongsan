<template>

<!-- <div class="black-bg" v-if="모달창열렸니==true">
  <div class="white-bg">
    <img :src="원룸들[누른거].image" style="width:100%">
    <h4>{{원룸들[누른거].title}}</h4>
    <p>{{원룸들[누른거].content}}</p>
    <button @click="모달창열렸니=false">닫기</button>
  </div>
</div> -->


<!-- <p>HTML속성에 데이터바인딩하려면 :속성="데이터이름"</p> -->

<!-- <dev class="start" :class="{end: 모달창열렸니}">  
<Modal @closeModal="모달창열렸니=false" :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니" />
</dev> -->

<transition name="fade">
<Modal @closeModal="모달창열렸니=false" :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니" />
</transition>


<div class='menu'>
  <a v-for="(a,i) in 메뉴들" :key="i">{{a}}</a>
</div>


<Discount v-if="showDiscount==true" />

<!-- <Discount></Discount> -->
<!-- <div class="discount">
  <h4>지금 결제하면 20% 할인</h4>
</div> -->


<button @click="priceSort">가격순정렬</button>
<button @click="sortBack">되돌리기</button>


<Card @openModal="모달창열렸니=true; 누른거=$event" :원룸="원룸들[i]" v-for="(a,i) in 원룸들" :key="i" />


  <!-- <div v-for="(a,i) in 원룸들" :key="i">
    <img :src="a.image" class='room-img'>
    <h4 @click="모달창열렸니=true; 누른거=i">{{a.title}}</h4>
    <p>{{a.price}}원</p>
  </div> -->


  <!-- <div v-for="(a,i) in products" :key="i">
    <h4>{{a}}</h4>
    <p>50 만원</p>
  </div> -->

  <!-- <div v-for="(a,i) in products" :key="a">
    <img src='./assets/room0.jpg' class='room-img'>
    <h4 @click="모달창열렸니=true">{{products[i]}}</h4>
    <p>50 만원</p>
    <button @click="신고수[i]++">허위매물신고</button> <span>신고수: {{신고수[i]}}</span>
  </div> -->
 


</template>



<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';


export default {
  name: 'App',
  data() {
    return {
      showDiscount: true,
      원룸들오리지널: [...data],  // 복사본만듬
      누른거: 0,
      원룸들: data,
      모달창열렸니 : false,
      신고수: [0,0,0],
      메뉴들: ['Home', 'Shop', 'About'],
      products: ['역삼동원룸','천호동원룸','마포구원룸'],
    }
  },
  methods: {
    increase() {
      this.신고수++;
    },
    sortBack() {
      this.원룸들 = [...this.원룸들오리지널]; //복사본만들어대입
    },
    priceSort() {
      this.원룸들.sort(function(a,b){
        return a.price - b.price
      })
    },
  },

  // App.vue에 대한 라이프사이클 훅
  mounted() {
    setTimeout(()=>{
      this.showDiscount = false;
    }, 2000);
  },
  components: {  
    Discount: Discount,
    Modal: Modal,
    Card: Card,
  }
}
</script>

<style>

body {
  margin: 0
}
div {
  box-sizing: border-box
}


/* Fade로 나타나고 사라짐 */
.fade-leave-from {
  /* opacity: 0; */
  transform: translateY(0px);
}  
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  /* opacity: 1; */
  transform: translateY(-1000px);
}

.fade-enter-from {
  /* opacity: 0; */
  transform: translateY(-1000px);
}  
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  /* opacity: 1; */
  transform: translateY(0px);
}

/* 고전적인 방법(js)으로 나타나고 사라짐 효과 */
.start {
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
}

/* 다양한 스타일링 */
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

/* 원래 있던 부분 */
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

</style>

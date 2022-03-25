<template>

<div class="black-bg" v-if="모달창열렸니==true">
  <div class="white-bg">
    <img :src="원룸들[누른거].image" style="width:100%">
    <h4>{{원룸들[누른거].title}}</h4>
    <p>{{원룸들[누른거].content}}</p>
    <!-- <input @input="month = $event.target.value"> -->
    <!-- <textarea v-model = "month"></textarea> -->
    <!-- <input type="checkbox" v-model="month"> -->
    <input v-model="month">
    <input type="range" min="1" max="12">    
    <select v-model="month">
        <option>1</option>
        <option>6</option>
        <option>12</option>
    </select>
    <p>{{ month }}개월 선택함 : {{원룸들[누른거].price * month}}원</p>
    <button @click="$emit('closeModal')">닫기</button>
  </div>
</div>


</template>

<script>
export default {
    name: 'Modal-item',
    data() {
        return {
            month: 1,
            //month: 'texttext',  // 초기값이 중요
        }
    },
    watch : {
        month(v) {  // month데이터 변경시 실행됨
            if (v > 12) {
                alert('13이상 입력하지 마셈')
            }
        }
    },
    props: {  // 전달받은 항목 등록
        원룸들: Array,
        누른거: Number,
        모달창열렸니: Boolean,
    }

}
</script>

<style>

</style>
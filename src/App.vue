<template>
  <!-- 모달 구현부 -->
  <div class="black-bg" v-if="isModalOpen === true">
    <div class="white-bg">
      <button @click="isModalOpen=false">X</button>
      <h4>상세페이지임</h4>
      <p>상세페이지 내용임</p>
    </div>
  </div> 

  <div class="menu">
    <!-- v-for로 반복문 적용 -->
    <!-- item: 해당 인덱스 값, :key: 어떤게 인덱스 값인지 지정 -->
    <a v-for="item in menu" :key="item">
      {{ item }}
    </a>
  </div>

  <!-- i: 인덱스 -->
  <div v-for="(item, i) in rooms" :key="item">
    <img class="room-img" :src="item.image">
    <!-- 설정 스타일 적용 -->
    <h4 @click="isModalOpen=true" class="red" :style="textColor">
      <!-- 설정 데이터 적용 -->
      {{ item.id+1 }}. {{ item.title }}
    </h4>
    <p>{{ item.price }}원</p>
    <!-- v-on:click으로 클릭 이벤트 구현 -->
    <!-- @click으로도 표현가능 -->
    <button v-on:click="onReport(i)">허위매물신고</button>
    <!--
    <button v-on:mouseover="onReport(i)">허위매물신고</button>
    <button v-on:input="onReport(i)">허위매물신고</button>
    -->
    <span>신고수 : {{ reports[i] }}</span>
  </div>
</template>

<script>
// 데이터 import
import data from "./assets/oneroom.js";


export default {
  name: 'App',
 
  /**
   * 데이터 바인딩을 하는 이유
   * 1. 변경사항이 많은 데이터를 HTML에 하드코딩을 하면 나중에 변경이 어려움
   * 2. Vue.js가 제공하는 실시간 렌더링 기능에 이용
   */
  // 데이터 바인딩 구현부
  data() {
    return {
      // key : value 형태로 값을 지정
      isModalOpen : false,
      menu : [`Home`, `Shop`, `About`],
      textColor : `color : blue`,

      rooms : data,
      reports : [0, 0, 0, 0, 0, 0],
    }
  },

  // 함수 구현부
  methods : {
    // onModal(index) {
    //   if(isModalOpen === true) {
    //     return this.products[i];
    //   }
    // },
    onReport(index) {
      // 함수안에서 데이터 쓸땐 this.데이터명으로 표기할 것
      this.reports[index] += 1;
    },
  },

  // components: {
  // },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}

.white-bg {
  width: 100%; height: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

.menu {
  background: darkslateblue;
  padding:  15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 15%;
  margin-top: 40px;
}
</style>

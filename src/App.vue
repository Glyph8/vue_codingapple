<template>

  <div class="black-bg" v-if="모달창열렸나">
    <div class="white-bg">
      <h4>상세페이지</h4>
      <p>상세페이지 내용</p>
      <div><button @click="모달창열렸나 = false">닫기</button></div>
    </div>
  </div>

 
  <div class="menu">
    <!--이렇게 작성하기 귀찮다면..
    <a>Home</a>
    <a>Products</a>
    <a>About</a>
    -->
    <a v-for="아무렇게나이름짓기 in 메뉴들" :key="아무렇게나이름짓기">{{아무렇게나이름짓기}}</a>
  </div>
  
  <h1 :style = 파랑글씨>원룸샵</h1>
  
  <div v-for="(판매목록, i) in 원룸들" :key="i"> 
    <img class="room-img" :src = 판매목록.image >  
    <h4 class = "room-name" @click="modalOn">{{판매목록.title}}</h4>
    <p>{{판매목록.price}}원</p>
    <p>{{판매목록.content}}</p>
    <button @click="increase(i)">허위매물신고하기</button> <span>{{ 신고수[i] }}</span>
  </div>

</template>

<script>

import oneRoomData from './oneroom'

//import {apple, apple2} from './oneroom'; //import해놓고 쓰지 않으면 에러가 발생한다.
//단일 export된 값을 import 할 때의 변수명은 다르게 해도 된다.
//export { ~ } 는 똑같이 가져와야함.

export default {
  name: 'App',

  data(){
    return{
      //data보관함 -> ui의 상태를 담는다 -> state라고도 부른다.
      //자료 형식은 object -> {name : value, ~} 형식
      
      원룸들 : oneRoomData,

      모달창열렸나 : false,

      메뉴들 : ["HOME", "SHOP", "ABOUT"],
      prices : [50, 10, 70],
      파랑글씨 : 'color : blue',
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],      
      신고수 : [0, 0, 0],
      roomImage : [require('./assets/room0.jpg'), require('./assets/room1.jpg'), require('./assets/room2.jpg')],
    }
  },//comma 필수

  methods : {//vue에서 함수만들기
    increase(i){
      //신고수 += 1;
      this.신고수[i] += 1; //this를 써서 데이터를 불러와야한다.
    },

    modalOn(){
      this.모달창열렸나 = true;
    }
  },

  components: {
    
  }
}
</script>

<style>

body{
  margin : 0;
}

div {
  box-sizing: border-box;
}

.black-bg{
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed;
  padding: 20px;
}

.white-bg{
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img{
  width : 100%;
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

.menu{
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color : white;
  padding: 10px;
}

</style>

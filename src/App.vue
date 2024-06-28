<template>
  <div class="app">
    <header>
      <h1>The <strong>Movie</strong> Database</h1>
      <form class="search-box" v-on:submit.prevent="handleSearch">
        <input type="search" class="search-field" placeholder="찾을 영화를 입력해주세요"
        v-model="search_query">
        <!-- search가 text와 다른 점: 끝에 X눌러서 취소할 수 있음 -->
      </form>
    </header>
    <main>
      <div class="cards">
        <card v-for="(movie) in movieList" :a="movie"></card><!-- card 컴포넌트 만듦 -->
        <!-- a라는 이름으로 movie가 전달 -->

      </div>
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import card from './components/cards.vue' //card 컴포넌트 집어넣음
const movieList = ref([]);
const search_query = ref('')

const handleSearch = async () => {
  movieList.value = await fetch(`https://api.themoviedb.org/3/search/movie?query=${search_query.value}&include_adult=false&language=en-US&page=1&api_key=1477758e07d73d14e91d27a701ab2547`)
    .then(response => response.json())  //JSON을 입력으로 받아 파싱하여 JavaSript 객체를 생성
    .then(data => data.results)

  search_query.value=''/* 초기화 */
}



const popular = async ()=>{//결과값이 promise인 것들은 async 써줘야함. async는 function 앞에 사용
  movieList.value= await fetch('https://api.themoviedb.org/3/movie/popular?language=en-US&page=1&api_key=1477758e07d73d14e91d27a701ab2547') //fetch 명령어 앞에 await */
/* async function 함수명() {
await 비동기_처리_메서드_명();
} */

    .then(response => response.json())//json 파일을 입력으로 받아 파싱하여 js 객체를 생성
    .then(data => data.results)

    console.log('받은 데이터',movieList.value);
  }//전역 fetch() 메서드는 네트워크에서 리소스를 취득하는 절차를 시작하고, 응답이 사용 가능해지면 이행하는 프로미스를 반환
  popular()

</script>

<style lang="scss">
$color: #313131;
/*scss에서 변수 설정은 $로 시작  */

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}

header {
  padding: 50px 0;

  h1 {
    /* 중첩은 scss의 특징 중 하나 */
    color: #999;
    text-align: center;
    font-weight: normal;
    text-transform: uppercase;
    /* 모두 대문자로 */
    font-size: 42px;
    margin-bottom: 30px;

    strong {
      color: $color;
    }
  }
}

.search-box {
  display: flex;
  /* 부모가 자식한테 물려줄때 display */
  justify-content: center;
  padding: 0 30px;

  /* 창 가로로 줄이면 여백생기게 */
  .search-field {
    appearance: none;
    border: none;
    outline: none;
    /* search창 클릭시 나타나는 테두리 */
    padding: 15px;
    width: 100%;
    max-width: 600px;
    background-color: #f3f3f3;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    font-size: 20px;
    color: $color;

    &::placeholder {
      color: #aaa;
    }

    /* &는 input을 의미 */

    &:focus {
      /* search창 클릭하면 나옴 */
      background: $color;
      color: white;
    }
  }
}

main {
  max-width: 1200px;
  margin: auto;
  padding: 0 16px;

  .cards {
    display: flex;
    /* 수평으로 나열 */
    flex-wrap: wrap;
    /* 화면에 잘리지 않고 보기 좋게 줄바꿔 나열 */
  }
}</style>

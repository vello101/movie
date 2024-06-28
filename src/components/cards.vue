<template>
   <div class="card">
      <a v-bind:href="'https://www.themoviedb.org/movie/'+a.id">
         <figure>
            <img v-if='a.poster_path' :src="'https://image.tmdb.org/t/p/w600_and_h900_bestv2' + a.poster_path" :alt="a.title">

            <img v-else src="http://placehold.it/200x300/ddd/333?text=MoviePoster" alt="">
            <!-- 더미이미지/가로길이x세로길이 /배경색/글씨색?text=쓰고싶은말 -->
         </figure>
         <div class="text">
            <h3>{{ a.title }}</h3>
         </div>
      </a>
   </div>
</template>

<script setup>
const props = defineProps(['a'])
</script>

<style lang="scss" scoped>
$tablet: '(max-width: 860px)';
$mobile: '(max-width: 600px)';

   .card{
      width: 25%;
      padding: 16px;

      @media#{$tablet}{/* 반응형:
         웹 페이지가 모든 화면 크기와 해상도에서 잘 렌더링(웹사이트 코드를 사용자가 웹 사이트를 방문할 때 보게 되는 대화형 페이지로 바꾸는 웹 개발에 사용되는 절차)되도록 하면서도 사용성을 보장하는 웹 디자인 접근 방식*/
         width: 33.33%;
      }
      @media#{$mobile}{/* 반응형 */
         width: 50%;
      }
      a{
         display: block;
         text-decoration: none;  /* a태그라 언더라인 생김 */
         box-shadow: 0 4px 8px rgba(0,0,0,0.3);

         figure{
            width: 100%;
            height: 360px;
            overflow: hidden;
            margin: 0;
            img{
               width: 100%;
               height: 100%; /* 부모인 figure에 딱 맞게 100% */
               object-fit: cover;
               /* 콘텐츠의 가로세로비를 유지하면서, 요소 콘텐츠 박스를 가득 채웁니다. 서로의 가로세로비가 일치하지 않으면 객체 일부가 잘려나갑니다 */
               transition: 0.3s;
            }
         }

         .text{
            border: 1px solid gray;
            height: 80px;
            padding: 16px;
         }
         h3{
            color: #313131;
            font-size: 16px;
         }
      }
      &:hover img{transform: scale(1.1);}/* 마우스 포스터에 올려놓으면 포스터 커지게 */
      &:hover h3{color: forestgreen;}/* 카드 영화제목에 마우스 올려놓으면 */
   }
</style>
<template>
  <div class="detail_movie">
   <h2>{{ movie.Title }}</h2>
   <p>{{movie.Actors}}</p>
   <img :src="movie.Poster" class="image" alt="Movie Poster">
   <p>{{movie.Plot}}</p>
  </div>
</template>

<script>
import { onBeforeMount, ref } from 'vue'
import { useRoute } from 'vue-router'
import  setup  from '@/setup'
export default {
  setup(){
   const movie = ref({})
   const route = useRoute()
    onBeforeMount(()=>{
      fetch(`http://www.omdbapi.com/?apiKey=${setup.apiKey}&i=${route.params.id}&plot=full`)
      .then(resp=> resp.json())
      .then(data=>{
        movie.value = data
      
      }).catch(err=>console.log(err))
    })
  return {
    movie,
    route
  }
  }

}
</script>

<style lang="scss">
.detail_movie{
  padding: 16px;
background: #C9D6FF; 
background: -webkit-linear-gradient(to right, #E2E2E2, #C9D6FF);  
background: linear-gradient(to right, #E2E2E2, #C9D6FF); 

  h2{
    color:rgb(148, 141, 141);
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }
  .image{
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }
  p{
    color: #fff;
    font-size: 17px;
    line-height: 1.4rem;
  }

}
</style>
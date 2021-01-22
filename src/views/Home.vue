<template>
  <div class="home">
    <div class="card">
      <router-link to="/movie/tt0409591">
        <img src="https://images.pexels.com/photos/274937/pexels-photo-274937.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500" alt="" class="card-img">
        <div class="detail">
          <h3>Looking for your favorite Movie</h3>
          <p>
            Mini movie app that help you to search for your favorite film , know more detail about it.</p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="searchMovies()" class="box-search">
      <input type="text" v-model="search"  placeholder="what are you looking for ?">
      <button :disabled="!counter">Search</button>
    </form>
    <div class="movies_list">
     <div class="movie" v-for="movie in movies" :key="movie.imdbID">
       <router-link :to="'/movie/'+movie.imdbID" class="movie_link">
       <div class="product_img">
         <img :src="movie.Poster" alt="poster movie">
         <div class="type">{{movie.Type}}</div>
       </div>
       <div class="detail">
         <p class="year">{{ movie.Year }}</p>
         <h3>{{ movie.Title }}</h3>
       </div>
       </router-link>
     </div>
    </div>
  </div>
</template>

<script>
import { computed, ref } from 'vue'
import setup from '@/setup.js'
export default {
  setup(){
    const search = ref("")
    const movies = ref([])
    const searchMovies = () =>{
      if(search.value != ""){
       fetch(`http://www.omdbapi.com/?apiKey=${setup.apiKey}&s=${search.value}`)
       .then(resp=> resp.json())
       .then(data =>{
         movies.value = data.Search
         search.value = ""
       }).catch(err=>console.log(err))
      }
    }
    const counter = computed(()=>search.value.length > 0)
    return {
      search,
      movies,
      searchMovies,
      counter
    }
  }
  
}
</script>
<style lang="scss">

.home{
  .card{
    position: relative;
    .card-img{
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }
    .detail{
      position: absolute;
      left: 0;
      right: 0;
      bottom:0;
      background-color: rgba(0,0,0,0.5);
      padding: 16px;
      h3{
        color: rgb(155, 132, 132);
        margin-bottom: 16px;
      }
      p{
        color: #fff;
      }
    }
  }
  .box-search{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input{
      display: block;
      appearance: none;
      border:none;
      outline: none;
      background: none;
      border-radius: 4px;
      &[type="text"]{
        width: 100%;
        color: #fff;
        background: #496583;
        font-size: 20px;
        padding: 10px 16px;
        margin-bottom: 15px;
        transition: 0.4s;
        &::placeholder{
          color: #f3f3f3;
        }
        &:focus{
          box-shadow: 0 3px 6px rgba(0,0,0,0.5);
        }
      }
    }
    button{
        display: block;
      appearance: none;
      border:none;
      outline: none;
      background: none;
       border-radius: 4px;
       width: 100%;
       max-width: 300px;
       background-color: #3e8163;
       padding: 16px;
       color: #fff;
       text-transform: uppercase;
       transition: .4s;
       &:hover{
         cursor: pointer;
       }
       &:active{
                background-color: #426883;

       }
       &:disabled{
         opacity: 50%;
         cursor:not-allowed;
       }
      
    }
    
  

  }
  .movies_list{
    display: flex;
    flex-wrap: wrap;
    padding:0 8px;
    .movie{
      max-width: 50%;
      flex:1 1 50%;
      padding:16px 8px;
      .movie_link{
        display: flex;
        flex-direction: column;
        height: 100%;
        .product_img{
          position: relative;
          display: block;
          img{
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }
          .type{
            position: absolute;
            padding: 8px 16px;
            background: #42B883;
            color: #fff;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }
        .detail{
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;
          .year{
            color:#aaa;
            font-size:15px;
          }
          h3{
            color: #fff;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>

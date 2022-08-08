<template>
  <div class="home">
    <div class="feature-card">
      <router-link :to="{ path: '/movie/tt0100669' }">
        <img
          src="https://img.ecartelera.com/noticias/fotos/69500/69504/1.jpg"
          alt="spiderman"
          class="featured-img"
        />
        <div class="details">
          <h3>Test</h3>
          <p>
            Lorem Ipsum is simply dummy text of the printing and typesetting
            industry. Lorem Ipsum has been the industry's standard dummy text
            ever since the 1500s, when an unknown printer took a galley of type
            and scrambled it to make a type specimen book. It has survived not
            only five centuries, but also the leap into electronic typesetting,
            remaining essentially unchanged. It was popularised in the 1960s
            with the release of Letraset sheets containing Lorem Ipsum passages,
            and more recently with desktop publishing software like Aldus
            PageMaker including versions of Lorem Ipsum.
          </p>
        </div>
      </router-link>
    </div>


    <form @submit.prevent="searchMovies()" class="search-box">
      <input type="text" placeholder="What are you looking for?" v-model="search">
      <input type="submit" value="Search">
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="{path: '/movie/' + movie.imdbID}" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{movie.Type}}</div>
          </div>
          <div class="detail">
            <p class="year">{{movie.Year}}</p>
            <h3>{{movie.Title}}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import env from '../env.js'
export default {
  name: "HomeView",
  setup() {
    const search = ref("")
    const movies = ref([])

    const searchMovies = () => {
      if (search.value !== "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
        .then(response => response.json())
        .then(data => {
          movies.value = data.Search;
          search.value = "";
        })
      }
    }

    return {
      search,
      movies,
      searchMovies
    }
  }
};
</script>
<style lang="scss">
.feature-card {
  position: relative;

  .featured-img {
    display: block;
    width: 100%;
    height: 300px;
    object-fit: cover;
    position: relative;
    z-index: 0;
  }

  .details {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.6);
    padding: 16px;
    z-index: 1;

    h3 {
      color: #fff;
      margin-bottom: 16px;
    }

    p {
      color: #fff;
    }
  }
}
.search-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 16px;

  input {
    display: block;
    appearance: none;
    border: none;
    outline: none;
    background: none;

    &[type="text"] {
      width: 100%;
      color: #fff;
      background: #496583;
      font-size: 20px;
      padding: 10px 16px;
      border-radius: 8px;
      margin-bottom: 15px;
      transition: 0.4s;

      &::placeholder {
        text-align: center;
        color: #f3f3f3;
      }

      &:focus {
        box-shadow: 0 3px 6px rgba(0,0,0,0.2)
      }
    }

    &[type="submit"] {
      width: 100%;
      max-width: 300px;
      background: #42B883;
      color: #fff;
      padding: 16px;
      border-radius: 8px;
      text-transform: uppercase;
      transition: 0.4s;

      &:active {
        background: #3BB070;
      }
    }
  }
}
.movies-list {
  display: flex;
  flex-wrap: wrap;
  margin: 0 8px;

  .movie {
    max-width: 50%;
    flex: 1 1 50%;
    padding: 16px 8px;

    .movie-link {
      display: flex;
      flex-direction: column;
      height:100%;
    }

    .product-image {
      position: relative;
      display: block;

      img {
        display: block;
        width: 100%;
        height: 275px;
        object-fit: cover;
      }

      .type {
        position: absolute;
        left: 0;
        bottom: 16px;
        padding: 8px 16px;
        background: #42B883;
        color: #fff;
        text-transform: capitalize;
      }
    }
    .detail {
      background: #496583;
      padding: 16px 8px;
      flex: 1 1 100%;
      border-radius: 0 0 8px 8px;

      .year {
        color: #aaa;
        font-size: 14px;
      }

      h3 {
        color: #fff;
        font-weight: 600;
        font-size: 18px;
      }
    }
  }
}
@media only screen and (max-width: 600px) {
  .feature-card {
    .featured-img {
      height: 500px;
    }
    .details {
      padding: 10px;
    }
  }
}
</style>

<template>

<div class="container mx-auto ">
  <div class="flex justify-between border-b border-gray-500">
   </div>
   <MovieList>
</MovieList>
 </div>
</template>

<script>
// @ is an alias to /src
import { Api } from '@/Api'
import MovieList from '../components/MovieList.vue'

export default {
  name: 'home',
  components: { MovieList },

  methods: {

    getMessage() {
      Api.get('/')
        .then((response) => {
          this.message = response.data.message
        })
        .catch((error) => {
          this.message = error
        })
    },
    getMovies() {
      Api.get('/movies').then(response => {
        this.movies = response.data.movies
        console.log(response.date)
      })
    }
  },
  mounted() {
    const user = localStorage.getItem('user')
    if (!user) {
      this.$router.push({ name: 'login' })
      alert('Please log in first')
    }
  }
}
</script>

<style scoped>
* {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
box-sizing: border-box
}
/* body {
 background-image: url("../assets/solid-color-image.png");
 background-color: #cccccc;
} */

.container {
  list-style-type: none;
  margin: 0;
  padding: 0;
  object-fit: cover;
}
</style>

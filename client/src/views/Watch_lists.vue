<template>
  <div>
  <div class="container">
    <h2>Bored?.. Check out some of our watchlists!</h2>

      <ul v-if="layout === 'grid'" class="card-list">
        <li v-for="list in watch_lists" :key="list._id">
          <img class="image" src="../assets/playlist_movie_icon.png" alt="test"/>
          <div class="lists_info">
            <h3 class="list-title">{{ list.title }}</h3>
            <router-link class=btn :to="/watch_lists/ + list._id + /details/"> View list</router-link>
          </div>
        </li>
      </ul>
      <hr>

<hr>
    </div>
  </div>
</template>

<script>

import { Api } from '@/Api'

export default {

  name: 'Watch_lists',

  created() {
    this.getWatchLists()
  },

  mounted() {
    const user = localStorage.getItem('user')
    if (!user) {
      this.$router.push({ name: 'login' })
      alert('Please log in first')
    }
  },
  data() {
    return {
      layout: 'grid',

      watch_lists: {}
    }
  },

  methods: {

    getWatchLists() {
      Api.get('/watch_lists').then(response => {
        this.watch_lists = response.data.watch_lists
      }).catch(error => {
        this.watch_lists = error
        console.log(error)
      })
    },
    getListById() {
      Api.get('/watch_lists/' + this.$route.params.id)
        .then(response => {
          this.list = response.data.list
        })
        .catch(error => {
          this.list = {}
          console.log(error)
        })
    },
    addList(list) {
      this.watch_lists.push(list)
    }
    /*  createList() {
      Api.post('/watch_lists').then((response) => {
        this.watch_lists = response.data
        console.log(response.data)
      })
        .catch((error) => {
          console.error(error)
        })
    } */

  }
}

</script>

<style scoped>
* {
  font-family: monospace, Avenir, Helvetica, Arial, sans-serif;
}

h2{
  text-align: center;
  font-weight: 700;
  padding: 10px;
  margin-top: 5px;
  color: white;
  border: 2px solid;
}

.container{
flex-direction: column;
justify-content: center;
align-items: center;
width: 1280px

}
.list-title {
  border-radius: 10px;
  color:white;
  margin: 16px auto;
}
.image {
  width: 2000x;
  height: 200px;
  object-fit: cover;
  background-color: #eec3c0;
  padding:0.5em;

}
.btn {
background-color: #998998;
font-size: medium;
color: white;
font-size: 20px;
margin: 1em 0;
padding: 10px 20px;
border-radius: 12px;
transition-duration: 0.4s;
}
.btn:hover {
background-color: #998998;
color: white;
font-size: 22px;

}
.card-list{
margin: 2em;
display:grid;
list-style: none;
box-sizing: border-box;
text-align: center;
grid-template-columns: repeat(3, minmax(100px, 1fr));
}
@media only screen and (max-width: 1025px) {
  .container {
      width: 100%;
  }
  .card-list {
    grid-template-columns: repeat(2, minmax(100px, 1fr));
  }
}
@media only screen and (max-width: 920px) {
  .container {
      width: 100%;
  }
  .card-list {
    grid-template-columns: repeat(2, minmax(100px, 1fr));
  }
}
@media only screen and (max-width: 620px) {
  .card-list {
    grid-template-columns: repeat(1, minmax(100px, 1fr));
  }
}
ul{
 list-style: none
}
span {
  border: 2px solid;
}
</style>

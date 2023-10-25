<template>
  <div id="app" class="container">
    <SearchBar @inputChange="onInputChange"/>
    <VideoList :videos="videos"/>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import VideoList from './components/VideoList.vue';
import videosAPIMock from './mocks/videosAPIMock'
const API_KEY = 'AIzaSyBwJH-yPgWWz8OtIx4Ad6Uu9JrHlp4Ifac';

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList
  },
  data() {
    return {
      videos: []
    }
  },
  methods: {
    onInputChange(searchTerm) {
      axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
          key: API_KEY,
          type: 'video',
          part: 'snippet',
          q: searchTerm
        }
      })
      .then(response => {
        this.videos = response.data.items;
      })
      .catch(err => {
        console.log(err.message);
        if (err.response.status === 403) {
          this.videos = videosAPIMock;
        }
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
}
</style>

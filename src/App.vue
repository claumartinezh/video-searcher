<template>
  <div id="app" class="container">
    <SearchBar @inputChange="onInputChange"/>
    <div class="video-layout">
      <VideoDetail :video="selectedVideo"></VideoDetail>
      <VideoList @videoSelected="onVideoSelected" :videos="videos" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import VideoList from './components/VideoList.vue';
import VideoDetail from './components/VideoDetail.vue';
import videosAPIMock from './mocks/videosAPIMock'
const API_KEY = 'AIzaSyBwJH-yPgWWz8OtIx4Ad6Uu9JrHlp4Ifac';

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  data() {
    return {
      videos: [],
      selectedVideo: null
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
    },
    onVideoSelected(video) {
      this.selectedVideo = video;
    }
  }
}
</script>

<style>
  .video-layout {
    display: flex;
  }
</style>

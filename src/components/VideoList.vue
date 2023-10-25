<template>
  <ul class="list-group">
    <VideoListItem
      v-for="video in videos"
      :video="video"
      :key="video.etag"/>
  </ul>
</template>

<script>
import VideoListItem from './VideoListItem.vue';

export default {
  name: 'VideoList',
  components: {
    VideoListItem
  },
  props: {
    videos: Array
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
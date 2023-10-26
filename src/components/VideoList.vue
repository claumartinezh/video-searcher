<template>
  <ul class="list-group col-md-4">
    <VideoListItem
      v-for="video in videos"
      :video="video"
      :key="video.etag"
      @videoSelected="onVideoSelected"/>
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
  },
  methods: {
    onVideoSelected(video) {
      this.$emit('videoSelected', video);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
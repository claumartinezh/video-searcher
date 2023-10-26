<template>
  <li class="list-group-item media" @click="onItemClick">
    <img class="mr-3" :src="thumbnailUrl" />
    <div class="media-body">
      {{ video.snippet.title }}
    </div>
  </li>
</template>

<script>
export default {
  name: 'VideoListItem',
  props: {
    video: Object
  },
  computed: {
    thumbnailUrl() {
      return this.video.snippet.thumbnails.default.url;
    }
  },
  methods: {
    onItemClick() {
      this.$emit('videoSelected', this.video);
    }
  }
}
</script>

<style scoped>
  li {
    display: flex;
    cursor: pointer;
  }
  li:hover {
    background-color: #eee;
  }
</style>

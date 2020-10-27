<template>
  <div id="app" class="container">
    <search-bar
      @termChange="onTermChange"
    ></search-bar>
    <div class="main">
      <video-detail
      :video="videoSelected"
    ></video-detail>
    <VideoList
      :videos="videos"
      @videoSelect="onVideoSelect"
    ></VideoList>
    </div>
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue';
import VideoList from './components/VideoList.vue';
import VideoDetail from './components/VideoDetail.vue';
import axios from 'axios';
const API_KEY = 'AIzaSyB2PQM7O6sv5JaFWSKk4wdovtGZxQF6r20';


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
      videoSelected: null
    }
  },
  methods: {
    onVideoSelect(video){
      this.videoSelected = video;
    },
    onTermChange(search) {
      axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
          key: API_KEY,
          type: 'video',
          part: 'snippet',
          q: search
        }
      }).then(response => {
        this.videos = response.data.items;
      })
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.main {
  display: grid;
  grid-template-columns: 1fr 350px;
}
</style>

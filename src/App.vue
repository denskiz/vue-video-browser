<template>
  <div class="container">
    <h1>Video Search</h1>
    <h5>Search for Videos - Built with Vue.js & the YouTube API</h5>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
      <VideoDetail :video="selectedVideo" />
      <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";
const API_KEY = "AIzaSyAeIB5Shr8P14DsDhSfiuNllzeDBEFc6Fk";
export default {
  name: "App",
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  data() {
    return { videos: [], selectedVideo: null };
  },
  methods: {
    onVideoSelect(video) {
      this.selectedVideo = video;
    },
    onTermChange(searchTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            q: searchTerm
          }
        })
        .then(response => {
          this.videos = response.data.items;
        });
    }
  }
};
</script>

<style scoped>
h1 {
  text-align: center;
  margin-top: 17px;
  font-family: Ubuntu, Cantarell, Helvetica Neue, sans-serif;
}
h5 {
  text-align: center;
  font-size: 17px;
}
</style>
<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <div class="row">
            <VideoDetail :video="selectedVideo"></VideoDetail>
            <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
        </div>
    </div>
</template>

<script>
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";
import VideoDetail from "./components/VideoDetail";

import axios from "axios";

const API_KEY = "AIzaSyC51FJNBIOCT5pZbMYsqMy_6I4dzKiwprw";

export default {
    name: "App",
    data() {
        return {
            videos: [],
            selectedVideo: null
        };
    },
    components: {
        VideoList,
        VideoDetail,
        SearchBar
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
</style>

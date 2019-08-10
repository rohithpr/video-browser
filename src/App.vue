<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
    </div>
</template>

<script>
import SearchBar from "./components/SearchBar";
import VideoList from "./components/VideoList";

import axios from "axios";

const API_KEY = "AIzaSyC51FJNBIOCT5pZbMYsqMy_6I4dzKiwprw";

export default {
    name: "App",
    data() {
        return {
            videos: []
        };
    },
    components: {
        VideoList,
        SearchBar
    },
    methods: {
        onVideoSelect(video) {
            console.log(video)
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

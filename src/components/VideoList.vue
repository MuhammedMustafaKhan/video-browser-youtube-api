<template>
    <div>
        <ul class="list-group">
            <video-list-item 
                v-for="(video, index) in videos" 
                :key="index"
                :video="video"
                @videoSelect="onVideoSelect"
                >
            </video-list-item>
        </ul>
    </div>
</template>

<script>
import VideoListItem from './VideoListItem.vue'
export default {
    name: 'VideoList',
    props: ['videos'],
    components: {
        VideoListItem
    },
    methods: {
        onVideoSelect(video) {
            this.$emit('videoSelect', video);
        }
    },
}
</script>

<style>
   
</style>
<template>
        <!--<ul>
            videolist {{videos}}
            <li v-for="video in videos" :key="video.etag">
                {{video.snippet.description}}
            </li>
        </ul>-->

        <ul class="list-group col-lg-4">
            <VideoListItem
                @video-select="onVideoSelect" 
                :video="video" 
                v-for="video in videos" 
                :key="video.etag" />
        </ul>
</template>

<script>

/*function onVideoSelect(event) {
    console.log(event.target)
}

button.addEventListener('video-select',onVideoSelect)*/

import VideoListItem from './VideoListItem.vue'

export default {
    name:'VideoList',
    components:{
        VideoListItem,
    },
    props:{
        videos:{
            type:Array,

        }
    },
    methods:{
        onVideoSelect(video){
            console.log('VL:video Selected!',video.snippet.title)
            this.$emit('video-select',video)
        }
    },
}
</script>

<style>

</style>
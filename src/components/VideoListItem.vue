<template>
    <li @click="onVideoSelect" class="video-list-item list-group-item">
        <img :src="thumbnailUrl" class="mr-3" alt="youtube-thumbnail-image">
        <div class="media-body">
        {{video.snippet.title}}
        </div>
    </li>
</template>

<script>
export default {
    name: 'VideoListItem',
    props:{
        video:Object,
    },
    methods:{
        onVideoSelect(){
            console.log('VLI:Selected!')
            this.$emit('video-select',this.video)
        }
    },
    computed:{
        //함수지만 명사형->값으로 리턴될거라서
        thumbnailUrl() {
            return this.video.snippet.thumbnails.default.url
        }
    }
    
}
</script>

<style scoped>
li.video-list-item {
    display:flex;
    cursor:pointer;
}
li.video-list-item:hover {
    background-color:#eee;
}
.media-body {
    margin:auto 0;
}
</style>
<template>
  <div id="app">
  <!--<input type="text" v-model="dangerMsg">-->
  <!--v-text: <p v-text="dangerMsg"></p>-->
  <!--v-html: <p v-html="dangerMsg"></p>-->
    <SearchBar @input-change="onInputChange" />
    <div class="row">
      <VideoDetail :video="selectedVideo"/>
      <VideoList @video-select="onVideoSelect" :videos="videos"/>
    </div>
  </div>
</template>

<script>
//.env.local파일에 작성한 변수 명이 서버 최초 실행시에 process.env.변수명으로 자동설정. 단 접두사는 VUE_APP_
import axios from 'axios'
import SearchBar from '@/components/SearchBar.vue'
import VideoList from '@/components/VideoList.vue'
import VideoDetail from '@/components/VideoDetail.vue'
const YOUTUBE_API_KEY=process.env.VUE_APP_YOUTUBE_API_KEY
const YOUTUBE_API_URL="https://www.googleapis.com/youtube/v3/search"
export default {
  name: 'app',
  components: {
    SearchBar,
    VideoList,
    VideoDetail,
  },
  data(){
    return {
      dangerMsg:'',
      inputValue:'',
      videos:[],
      selectedVideo:null,
    }
  },

  methods:{
    onInputChange(userInput){
      const config = {
        params: {
          key:YOUTUBE_API_KEY,
          part:'snippet',
          type:'video',
          q:userInput,
        }
      }

      axios.get(YOUTUBE_API_URL,config)
      .then(res =>{
        //console.log(res.data.items)
        //this.videos=res.data.items
        res.data.items.forEach(item=>{
          const parser = new DOMParser()
          const doc = parser.parseFromString(item.snippet.title,'text/html')
          item.snippet.title = doc.body.innerText
        })
        this.videos = res.data.items
      })
      .catch(err =>{
        console.error(err)
      })
    },
    onVideoSelect(video){
      //console.log('App:받음!',video)
      this.selectedVideo = video
  },
  },
}
</script>

<style>

</style>

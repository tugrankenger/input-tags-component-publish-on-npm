<template>
  <div class="container">
    <app-tags v-model="tags" color="success"/>
    {{tags.toString().replaceAll(',',', ')}}
    <app-tags v-model="tags2" color="primary"/>
    {{tags2.toString().replaceAll(',',', ')}} 
  </div>
</template>

<script>
import Tags from './components/Tags.vue'
export default {
  components:{
    appTags: Tags
  },
  data(){
    return{
      tags:"Vuejs,React,Angular,Nodejs,Rust,Assembly",
      tags2 :"Python,Java,.Net"
    }
  }
}
</script>

<style>
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>
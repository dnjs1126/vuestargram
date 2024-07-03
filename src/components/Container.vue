<template>
<div>
  <Post :instaData="instaData"/>
</div>
</template>
<script>
import Post from "./Post.vue"
export default {
    name:"ContainerComponent",
    components:{
        Post,
    },
    props:{
        instaData : Array
    },
}
</script>
<style>
    
</style>
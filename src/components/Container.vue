<template>
    <div>
        <div v-if="step == 0">
            <Post :instaData="instaData" />
        </div>
        <!-- 필터선택페이지 -->
        <div v-if="step == 1">
            <div class="upload-image" :style="{ backgroundImage : `url(${img})`}"></div>
            <div class="filters">
                <div class="filter-1"></div>
                <div class="filter-1"></div>
                <div class="filter-1"></div>
                <div class="filter-1"></div>
                <div class="filter-1"></div>
            </div>
        </div>

        <!-- 글작성페이지 -->
        <div v-if="step == 2">
            <div class="upload-image" :style="{ backgroundImage : `url(${img})`}"></div>
            <div class="write">
                <textarea class="write-box" @input="$emit('write',$event.target.value)">write!</textarea>
            </div>
        </div>

    </div>
</template>
<script>
import Post from "./Post.vue"
export default {
    name: "ContainerComponent",
    components: {
        Post,
    },
    props: {
        instaData: Array,
        step: Number,
        img : String
    },
  

}
</script>
<style>
.upload-image {
    width: 100%;
    height: 450px;
    background: cornflowerblue;
    background-size: cover;
}

.filters {
    overflow-x: scroll;
    white-space: nowrap;
}

.filter-1 {
    width: 100px;
    height: 100px;
    background-color: cornflowerblue;
    margin: 10px 10px 10px auto;
    padding: 8px;
    display: inline-block;
    color: white;
    background-size: cover;
}

.filters::-webkit-scrollbar {
    height: 5px;
}

.filters::-webkit-scrollbar-track {
    background: #f1f1f1;
}

.filters::-webkit-scrollbar-thumb {
    background: #888;
    border-radius: 5px;
}

.filters::-webkit-scrollbar-thumb:hover {
    background: #555;
}

.write-box {
    border: none;
    width: 90%;
    height: 100px;
    padding: 15px;
    margin: auto;
    display: block;
    outline: none;
}
</style>
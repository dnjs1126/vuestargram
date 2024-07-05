<template>
  <div>
    <div class="header">
      <ul class="header-button-left">
        <div v-if="step>0">
          <li @click="step--">Cancel</li>
        </div>
      </ul>
      <ul class="header-button-right">
        <div v-if="step<2">
          <li @click="step++">Next</li>
        </div>
        <li v-if="step == 2" @click="publish">발행</li>
      </ul>
      <img src="./assets/logo.png" class="logo" />
    </div>
    
    <button @click="step = 0">버튼1</button>
    <button @click="step = 1">버튼2</button>
    <button @click="step = 2">버튼3</button>
    
    <Container :instaData="instaData" :step="step" :img="img" @write="write=$event"/>
    
    <button class="the" @click="more">더보기</button>
    
    <div class="footer">
      <ul class="footer-button-plus">
        <input @change="upload" type="file" id="file" class="inputfile" />
        <label for="file" class="input-plus">+</label>
      </ul>
    </div>
  </div>
</template>

<script>
import Container from './components/Container.vue';
import data from './assets/data.js'
import axios from 'axios';
export default {
  data() {
    return {
      step: 0,
      instaData:data,
      clickNum:0,
      img: '',
      write:'',
    };
  },
  methods:{
    more(){
      axios.get(`https://codingapple1.github.io/vue/more${this.clickNum}.json`)
        .then(result=>{
          console.log(this)
          this.instaData.push(result.data)
          this.clickNum++;
        })
        .catch(err=>{
          console.log(err)
        })
    },
    upload(e){
      let file = e.target.files;
      console.log(file)
      let url = URL.createObjectURL(file[0]);
      this.img=url;
      this.step++;
    },
    publish(){
      let myPost = {
        name: "Kim Hyun",
        userImage: "https://picsum.photos/100?random=3",
        postImage: this.img,
        likes: 36,
        date: "May 15",
        liked: false,
        content: this.write,
        filter: "perpetua"
      };
      this.instaData.unshift(myPost);
      this.step=0;
    }
  },
  components: {
    Container,
  },
}
</script>

<style>
body {
  margin: 0;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
.the{
  border: none; 
  background-color: skyblue; 
  color: white; 
  padding: 5px 5px;
  font-size: 13px; 
  cursor: pointer;
  border-radius: 5px; 
  outline: none; 
}

.the:hover {
  background-color: #007bff; 
}
</style>


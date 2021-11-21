<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- background mask -->
  <div class="full-page mask" ></div>
  <div class="full-page background-img" >
    <DashBoard/>
  </div>


  <!-- mock -->
  <div id="top-menu" >
    <div class="nav-bar">
      <div class="nav-bar-item" v-for="men in menus" v-bind:key="men.id" > 
        <Button :label="men.name" class="p-button-outlined p-button-secondary events-btn" style="color:white;font-size:25px" />
      </div>
    </div>
    <div class="logo">
      <img class="img-full" src="./assets/images/logos/transparent_logo.png" alt="">
    </div>
  </div>

  <div id="footer" >
    <p>STOPKA</p>
  </div>

  <div class="events">
    
    <div id="sports-events" >

      <div class="img-full-container" >
        <img class="img-full" src="./assets/images/backgrounds/sports.jpg" alt="">
      </div>
      <Button label="WYDARZENIA SPORTOWE" class="p-button-outlined p-button-secondary events-btn" style="color:white" />

    </div>

    <div id="music-events" >
      <div class="img-full-container" >
        <img class="img-full" src="./assets/images/backgrounds/music.jpg" alt="">
      </div>
      <Button label="IMPREZY" class="p-button-outlined p-button-secondary events-btn" style="color:white" />

    </div>


  </div>


</template>

<script>
import DashBoard from './components/DashBoard.vue'
import Button from 'primevue/button';

export default {
  name: 'App',
  components: {
    DashBoard,
    Button
  },
  data () {
    return {
      menus:[
      {
        id:1,
        name:"Galeria"
      },
      {
        id:2,
        name:"Kontakt"
      },
      {
        id:2,
        name:"Cośtam"
      },
      {
        id:2,
        name:"Cośtam"
      },
      {
        id:2,
        name:"Cośtam"
      }

      ]
    }
  }
}
</script>

<style>
p{
  font-size:20px
}
.nav-bar{
    /* background-color: white; */
    position: absolute;
    width: 60%;
    /* height: 70%; */
    z-index: 2;
    top: 50%;
    left: 20%;
    color: white;
    display: inline-flex;
}
.nav-bar-item{
  margin-left:3%
}
.img-full-container{
    margin-top: 25%;
    transition: all 1s;
    cursor: pointer;
    background: blue;
    overflow: hidden;
    position: relative;
    height: 60%;  
}
.img-full{
    width:-webkit-fill-available;
    height:-webkit-fill-available;
    transition: all .5s;
}
.img-full:hover{
    transform: scale(1.1);
}
.events-btn{
  width: 99%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}
#footer{
  /* background:green; */
  width: 99%;
  height: 5%;
  position: fixed;
  bottom:10px
}
#top-menu{
  /* background:yellow; */
  border-bottom: solid rgb(150, 147, 147) 1px;
  width: 100%;
  height: 12%;
  position: fixed;
  left: 0
}
.logo{
  /* background-color:rgb(0, 102, 255); */
  width: 10%;
  position: relative;
  left: 80%;
}
.events{
  position: absolute;
  width: 70%;
  height: 70%;
  z-index: 2;
  top: 20%;
  left: 15%;
  /* background: red; */
  display: flex;
}
#sports-events{
  /* background:blue; */
  width: 40%;
  height: 100%;
  margin-left: 10%;
}
#music-events{
  /* background:pink; */
  width: 40%;
  height: 100%;
}

.full-page{
  /* Full height */
  height: 100%;

  /* Center and scale the image nicely */
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;

  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  
}
.background-img{
  background-image: url('assets/images/backgrounds/football-background.jpg');
  z-index:-2

}
.mask{
  background-color: black;
  z-index: -1;
  opacity:0.4
}
</style>

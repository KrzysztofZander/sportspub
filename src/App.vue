<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> :src="'/../assets/images/logos/'+events[selectedEnevetId-1].img -->
  <!-- background mask -->
  <div class="full-page mask" ></div>
  <div class="full-page background-img" >
    <DashBoard/>
  </div>


  <!-- mock -->
  <div class="wrapper">
    <!-- HEAD -->
    <div class="header">
      <div class="h1 h-menu">
        <div  class="menu-items" >
            <div  :class="'main-text-items selected-'+[selectedNavItemId == m.id]" v-for="m in menus.slice(0, 2)" :key="m.id" >
              <span  @click="selectedNavItemId = m.id"> {{ m.name }}  </span>
            </div>
        </div>
      </div>
      <div class="h2">
        <div class="logo">
          <img alt="" src="./assets/images/logos/transparent_logo.png">
        </div>
      </div>
      <div class="h3 h-menu">
        <div  class="menu-items" >
            <div  :class="'main-text-items selected-'+[selectedNavItemId == m.id]" v-for="m in menus.slice(2, 4)" :key="m.id" >
              <span  @click="selectedNavItemId = m.id"> {{ m.name }}  </span>
            </div>
        </div>
      </div>
    </div>

    <!-- MAIN -->
    <div  class="main">
      <div v-if="selectedNavItemId == 1" class="main-home" >
        <div class="main-foto img-full-container" >
            <img class="img-full in-border" alt="" v-bind:src="require('./assets/images/logos/' + events[selectedEnevetId-1].img)"  >
        </div>
        <div class="main-text main-title">
          {{ events[selectedEnevetId-1].title }}
        </div>
        <div class="main-text main-text-text">
          <span >
            {{ events[selectedEnevetId-1].text }}
          </span>
        </div>
        <div class="main-res" > 
          <Button label="REZERWACJA" />
        </div>
        <div class="main-ind">
            <div v-for="event in events" v-bind:key="event.id" >
              <Button @click="changeEvent(event.id)" v-if="event.id == selectedEnevetId"  class="p-button ind-btn" />
              <Button @click="changeEvent(event.id)" v-else  class="p-button-secondary ind-btn" />
            </div>
        </div>
      </div>

      <div v-if="selectedNavItemId == 4" class="main-contact" >
        
        <div class="main-content" >
          <div class="map">
            <GoogleMap
              :api-key="googleApiKey"
              style="width:100%; height:100%"
              :center="center"
              :zoom="15"
              >
                <Marker :options="{ position: center }" />
            </GoogleMap>
          </div>
          <div class="contact-form" >
            <div class="contact-title">
              Skontaktuj się z nami
            </div>
            <div class="contact-address contact-prop">
              Księdza Leona Miszewskiego 12/13
              <br> 80-239 Gdańsk

            </div>
            <div class="contact-n-week contact-prop">
              Pon. - Czw. 16:00 – 00:00
            </div>
            <div class="contact-week contact-prop">
              Pt. - Sob. 16:00 – 02:00
            </div>
            <div class="contact-phone contact-prop">
              <i class="pi pi-phone" style="font-size: 1.2vw; margin-right:5%;"/>609 260 113
            </div>
            <div class="contact-email contact-prop">
              sportspub@pub.com
            </div>
            <div class="contact-facebook contact-prop">
              <div>
                <i class="pi pi-facebook" style="font-size: 2vw; width:30%;float:left;color:#4267B2"/>
                <i class="pi pi-instagram" id="insta" style="font-size: 2vw; width:30%;float:left"/>
                <i class="pi pi-twitter" style="font-size: 2vw; width:30%;float:left;color:#1DA1F2"/>
                
              </div>
            </div>

          </div>

        </div>
      </div>

      <div v-if="selectedNavItemId == 2" class="main-calendar" >
        <div class="main-content"> 
          <div class="calendar-calendar" >
            <Calendar style="width:100%;height:100%; background:unset" v-model="value" dateFormat="dd.mm.yy" :inline="true" />
          </div>
          <div class="calendar-events" >
            <Carousel :value="cars">
              <template #item="slotProps">
                {{ slotProps.data }}
              </template>
            </Carousel>
          </div>
        </div>
      </div>


    </div>

    <!-- FOOT -->
    <div class="footer">
      <div v-if="selectedNavItemId == 1" class="fotter-home" >
        <div class="sports">
          <div class="img-full-container in-footer">
            <img class="img-full" src="./assets/images/backgrounds/colors.png" alt="">
          </div>
        </div>
        <div class="musics">
          <div class="img-full-container in-footer">
            <img class="img-full" src="./assets/images/backgrounds/musics2.png" alt="">
          </div>
        </div>
        <div class="footer-btn-sports" >
            <Button label="WYDARZENIA SPORTOWE"/>
        </div>
        <div class="footer-btn-musics" >
            <Button label="WYDARZENIA MUZYCZNE"/>
        </div>
      </div>
      
    </div>

  </div>

  <div style="display:none" >
    <Button/>
    <Calendar v-model="value" dateFormat="dd.mm.yy" />
  </div>




</template>

<script>
import DashBoard from './components/DashBoard.vue';
import Button from 'primevue/button';
import { GoogleMap, Marker } from 'vue3-google-map';
import Calendar from 'primevue/calendar';


export default {
  name: 'App',
  components: {
    DashBoard,
    Button,
    GoogleMap,
    Marker,
    Calendar
  },
  data () {
    return {
      selectedEnevetId:1,
      selectedNavItemId:1,
      center:{ lat: 54.3770562, lng: 18.6147892 },
      googleApiKey:null,
      menus:[
      {
        id:1,
        name:"Home"
      },
      {
        id:2,
        name:"Kalendarz"
      },
      {
        id:3,
        name:"Galeria"
      },
      {
        id:4,
        name:"Kontakt"
      }

      ],
      events:[
        {
          id:1,
          img:"dyskoteka.jpg",
          text:'W każdą sobotę zapraszamy Was wszystkich , czyli sportowych i muzycznych pasjonatów, w muzyczną podróż do lat 80/90/2000 jak i współczesnych.\nZapraszamy pod wiele mówiącym hasłem "DYSKOTEKA DOROSŁEGO CZŁOWIEKA" - muzyczny mix największych klubowych przebojów ostatnich 40 lat - coś czego brakuje na klubowej mapie Trójmiasta, a co dajemy Wam co sobotę w wykonaniu jednej z ikon trójmiejskich dyskotek i klubów, rezydenta m.in. takich miejsc jak MECHANIK, METRO, MAX, VIVA SOPOT, JAŚKOWA DOLINA 14, AVIATOR czyli DJ Grosheck - człowieka, który nieprzerwanie bawi Was od ponad 20 lat.\nNie możesz się doczekać - SUPER - My Też !!!!  ',
          title:"WYDARZENIE MUZYCZNE"
        },
        {
          id:2,
          img:"legia-napoli.jpg",
          text:"ZAPRASZAMY DO WSPÓLNEGO OGLĄDANIA MECZU LIGI EUROPY \n LEGIA WARSZAWA - NAPOLI",

          title:"WYDARZENIE SPORTOWE"
        },
        {
          id:3,
          img:"hallo.jpg",
          text:"HALLO GRUPOWICZE I KLUBOWICZE\
                *******************************************\
                HALLOWEEN ZBLIŻA SIĘ WIELKIMI KROKAMI I MY JUŻ JESTEŚMY NA NIE GOTOWI.\
                ********************************************\
                MUZYCZNA UCZTA DLA WSZYSTKICH MIŁOŚNIKÓW MUZYCZNYCH KLIMATÓW LAT 90 A PRZY OKAZJI MOJE URODZINY - MAM NADZIEJĘ, ŻE WAS NIE ZABRAKNIE\
                ********************************************\
                WJAZD: 10 ZŁ\
                DRESS CODE: CASUAL ELEGANCE\
                PROMOCJE NA BARZE DO 24:00\
                GODZ 21.00\
                ********************************************",
          title:"WYDARZENIE OKOLICZNOŚCIOWE"
        },
        {
          id:4,
          img:"depeche.jpg",
          text:"SportPub zaprasza na halloweenową noc z muzyką zespołu Depeche Mode w piątek 29.10.2021.\
                Tego wieczoru nie dajcie się prosić i przybywajcie do nas  w przebraniu ( mile widziane) lub bez. Najlepiej przebrana osoba zostanie nagrodzona w barze ;)\
                Obraz ( na dużym ekranie i kilku mniejszych zsynchronizowanych ze sobą )  i dźwięk dostarczy Radek aDHd.\
                Imprezę zaczynamy od 21:00,\
                koniec przewidujemy ok. 4:00.\
                Wstęp: 10 zł.",

          title:"WYDARZENIE TEMATYCZNE"
        }
      ],
      responsiveOptions: [
        {
          breakpoint: '1024px',
          numVisible: 3,
          numScroll: 3
        },
        {
          breakpoint: '600px',
          numVisible: 2,
          numScroll: 2
        },
        {
          breakpoint: '480px',
          numVisible: 1,
          numScroll: 1
        }
      ],
      cars:[
        {
          data:'1'
        },
        {
          data:'2'
        }
      ]
    }
  },
  mounted () {
    this.startEventInteraval()
    
  },
  created () {
    this.googleApiKey = process.env.VUE_APP_GOOGLE_MAP_API_KEY
  },
  methods: {
    startEventInteraval(){
      this.interval = setInterval(this.nextEvent, 8000)
    },
    nextEvent(){
      this.selectedEnevetId++
      if( this.selectedEnevetId > this.events.length )this.selectedEnevetId=1
    },
    changeEvent(id){
      clearInterval( this.interval )
      this.selectedEnevetId = id
      this.interval = setInterval(this.nextEvent, 8000)
    }
  }
}
</script>

<style>
p{
  font-size:20px
}
body{
    background: black;
}
.map{
    width: 64%;
    height: 79%;
    float: left;
}
#insta {
  background: radial-gradient(circle at 30% 107%, #fdf497 0%, #fdf497 5%, #fd5949 45%, #d6249f 60%, #285AEB 90%);
  -webkit-background-clip: text;
          /* Also define standard property for compatibility */
          background-clip: text;
  -webkit-text-fill-color: transparent;
  
  font-size: 200px; /* change this to change the size*/
  
}
.fotter-home{
  display: grid;
  grid-row:1/5;
  grid-column:1/6;
}
.main-home{
  grid-column: 1/11;
  grid-row: 1/11;
  display: grid;
  grid-template-columns: repeat(10, 1fr);
  grid-template-rows: repeat(10, 1fr);
}
.main-contact{
  margin-top: 2%;
  grid-column: 1/11;
  grid-row: 1/11;
  display: grid;
  grid-template-columns: repeat(10, 1fr);
  grid-template-rows: repeat(10, 1fr);
}

.contact-form{
  float: right;
  width: 35%;
  height: 90%;
  display: grid;
  grid-template-rows: repeat(22, 1fr);
}
.contact-prop{
  font-weight: 600;
  font-size: 1VW;
  color:white;

}
.contact-title{
  grid-row: 3;
  color:#2196f3 ;
  font-weight: 600;
  font-size: 1.6VW;
}
.contact-address{
  grid-row: 5;
}
.contact-n-week{
  grid-row: 6;
}
.contact-week{
  grid-row: 7;
}
.contact-phone{
    grid-row: 9;
}
.contact-email{
    grid-row: 10;
    color:#2196f3 ;
}
.contact-facebook{
    grid-row: 19;
    margin-right:35%;
    margin-left:2%;
    color:#2196f3 ;
    cursor: pointer;
}
.main-content{
    /* border: solid white; */
    width: 67vw;
    height: 67vh;
}
.calendar-calendar{
  /* border: solid red; */
  width:50%;
  height:100%;
  float:left;
}
.calendar-calendar div{
  background: #00000096;
  color: white;
  border: unset;

}
.calendar-calendar span:hover{
  color: black;
}
.p-datepicker-header{
  background: #00000096 !important;
}
.p-link{
  color: white !important
}
.calendar-events{
  background: #00000096;
  color: white;
  float: right;
  border: solid red;
  width:50%;
  height:100%;
  display: grid;
  grid-template-columns: repeat(4,1fr);
  grid-template-rows: repeat(5,1fr);

}
.in-footer{
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
}
.in-footer img{
  width:100%;
  height:100%
}

.events{
    width: 50%;
    margin: unset;
    background: white;
}
.ind-btn{
  height:10px;
  margin-left:10px !important;
}
.selected-true{
  color: #2196f3 !important;
}
.wrapper {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: grid;
  border-style: solid;
  /* border-color: red; */
  grid-template-columns: repeat(6, 1fr);
  grid-template-rows: repeat(8, 1fr);
  grid-gap: 10px;
}
.header {
  grid-column: 2/6;
  grid-row: 1;
  display: grid;
  grid-template-columns: repeat(20, 1fr);
  grid-template-rows: repeat(1, 1fr);

}
.h-menu{
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(3, 1fr);
}
.menu-items{
  grid-column: 1/8;
  grid-row:2;
  border-bottom: solid white;
  display: flex;
  align-items: flex-end;

}
.h1{
  grid-column: 1/8;
}
.h2{
  grid-column: 8/14;
}
.logo{
  display: flex;
  height: 100%;
  
}
.h2 img{
    align-self: flex-end;
    display: inline-block;
    margin-left: auto;
    margin-right: auto;
    width: 80%;
}
.h3{
  grid-column: 14/21;
}
.border-img{
  width:100%
}
.in-border{
  position: relative
}
.main-text-items{
  color:white;
  font-weight:600;
  text-align: center;
  font-size: 1.6VW;
  width:50%;
  cursor: pointer;
}
.main{
  /* border: solid white; */
  /* border-style: solid; */
  grid-column: 2/6;
  grid-row: 2/6;
  display: grid;
  grid-template-columns: repeat(10, 1fr);
  grid-template-rows: repeat(10, 1fr);

}
.main-foto {
  grid-column: 1/8;
  grid-row: 1/10;

}
.main-ind{
  grid-column: 1/8;
  grid-row: 10/10;
  /* border: solid red; */
  display: flex;
  align-self: center;
  margin:auto;
}
.main-title{
  grid-column: 8/11;
  grid-row: 1/3;
  font-size: 1.6VW;
  /* border: solid rgb(229, 255, 0) */
}
.main-text-text{
  grid-column: 8/11;
  grid-row: 3/10;
  /* border: solid rgb(0, 255, 64) */
}
.main-res{
  grid-column: 8/11;
  grid-row: 10/11;
  text-align: center;
  /* border: solid rgb(89, 0, 255); */
}
.main-res button{
  width: 100%;
}
.main-text{
  color:white;
  font-weight:600;
  text-align: center;

}
.footer {
    grid-column: 2/6;
    grid-row: 6/9;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(4, 1fr);

}
.sports{
    grid-column: 1/3;
    grid-row: 1/4;
    position: relative;
    margin: 0 12%;
}
.sports-foto{
    position: absolute;
    right: 0;
    top: 0

}
.footer-btn-sports{
    grid-column: 1/3;
    grid-row: 4/5;
    margin: 0 12%;
}
.footer-btn-musics{
    grid-column: 3/5;
    grid-row: 4/5;
}
.footer button{
    width: 100%;
    margin-top: 2%;    
}
.musics{
  /* border: white solid; */
  grid-row: 1/4;
  grid-column: 3/5;
  position: relative;
  margin: 0% -2%;

}
.musics-foto{
    position: absolute;
    left: 0;
    top: 0
}
.img-full-container{
    transition: all 1s;
    border: solid white;
    cursor: pointer;
    display:flex;
    overflow: hidden;
    float: left;
    margin-left: auto;
    margin-right: auto;
    max-width: -webkit-fill-available;
    border-radius: 5%
}
.img-full{
    transition: all .5s;
    margin-left: auto;
    margin-right: auto;
    max-width: -webkit-fill-available;
}
.img-full:hover{
    transform: scale(1.1);
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
  background-image: url('assets/images/backgrounds/black_bcg.jpg');
  z-index:-2

}
.sports-background-img{
  background-image: url('assets/images/backgrounds/colors.png');
  z-index:-2

}
.mask{
  background-color: black;
  z-index: -1;
  opacity:0.6
}
</style>

<template>
  <div class="container">
    <div class="container pbox" id="pbox">
<div class="mt-5"></div>

<div class="buttons">
    <div class=toptop>
<select name="estados" class="custom-select" required v-model='prueba' @change="selectState()">
    <option v-for="estado in estados" :key="estado.id">{{estado}}</option>
</select>

<select name="ciudades" class="custom-select" v-model='city' @change="getwh()">
    <option  v-for="city in cities" :key="city.id">{{city}}</option>
</select>
</div>
<div class="container-button toptop">  
 
<div><div id="ball" @click="changeTheme()" class="ball">.</div></div>

</div>
</div>

<div class="main1">
<i class="wi size-5rem icont" :class="newIcon" ></i>

<div>
<div class="fnt3">{{main.temp}}°C</div>
<div class="fnt2">{{clima.description}}</div>
</div>
</div>

<div class="secondInfo">

<div class="secondInfoch">
<i class="wi size-1rem icont wi-strong-wind fnt1"  ></i>
<p class="textinfo">{{wind.speed}} Km/m &nbsp; &nbsp;</p>
</div>


<div>
<i class="wi size-1rem icont wi-thermometer-exterior fnt1"  ></i>
<p class="textinfo">{{main.temp_max}}°C &nbsp; &nbsp;</p>
</div>


<div>
<i class="wi size-1rem icont wi-thermometer fnt1"  ></i>
<p class="textinfo">{{main.temp_min}}°C &nbsp; &nbsp;</p> 
</div>

</div>











</div>
</div>
</template>   




<script>
import Logo from '~/components/Logo.vue'
import axios from 'axios'
import states from 'assets/js/states.js'
import iconos from 'assets/js/icons.js'
export default {
  head: {
    bodyAttrs: {
      id: 'bdy'
    }
  },
  data(){
    return{
      cities:'',
      clima: '',
      main:'',
      wind:'',
      estados:['Aguascalientes','Baja California','Baja California Sur','Campeche','Coahuila de Zaragoza','Colima','Chiapas','Chihuahua','Distrito Federal','Durango','Guanajuato','Guerrero','Hidalgo','Jalisco','México','Michoacán de Ocampo','Morelos','Nayarit','Nuevo León','Oaxaca','Puebla','Querétaro','Quintana Roo','San Luis Potosí','Sinaloa','Sonora','Tabasco','Tamaulipas','Tlaxcala','Veracruz de Ignacio de la Llave','Yucatán','Zacatecas'],
      cities:'',
      city:'Aguascalientes',
      estadoss:states,
      prueba:'Aguascalientes',
      icons:iconos,
      newIcon:''

  }},
  created(){
   // this.getcities()
     this.getwh()

  },
  mounted(){
  },
  methods:{
    changeTheme(){
      var element = document.getElementById("ball");
       element.classList.toggle("darktheme");

      var element2 = document.getElementById("pbox");
       element2.classList.toggle("darksquare");
       
       var element3 = document.getElementById("bdy");
       element3.classList.toggle("darkb");

    },
    
    selectState(){

      const currentState = this.prueba
      const cities = states.estado.find(state=>{
        return state.nombre === currentState
      })
      if(!cities){
         return alert('no esta la ciuda')
      }
      //console.log(cities)
      this.cities = cities.ciudades
    },
getwh() {
    
      const url = 'https://api.openweathermap.org/data/2.5/weather?q='+this.city+'&units=metric&appid=74809c652a768472e95f5d913143d783'
      const params={
          id:'2172797',
          appid:'74809c652a768472e95f5d913143d783'
      }
      axios
        .get(url,params)
        .then((response) => {
          this.clima = response.data.weather[0]
          this.main = response.data.main
          this.wind = response.data.wind

        
        const oldIcon= this.clima.icon
        const newIcon = iconos.iconos.find(ic=>{
          return ic.current == oldIcon
        })
        this.newIcon=newIcon.new
        





        })
        .catch(() => {
          alert('error')
        })
    },

  
  getcities() {
      const url = 'https://inegifacil.com/cities/3'
      axios
        .get(url)
        .then((response) => {
          this.cities = response.data
        })
        .catch(() => {
          alert('error')
        })
    },

},
components:{
  states,
  iconos
}

}
</script>

<style>
.pbox{
  background:#f3f4f3;
  width: 60%;
  border-radius: 30px;
}
.container-button{
  width: 50px;
  height: 26px;
  border-radius: 50px;
  background:grey;
  display:inline-block;

}
.ball{
  background:white;
  width:24px;
  height: 26px;
  margin:2px;
  border-radius: 50px;
  color:white;
}

.darktheme{
  transform: translate(20px);
}


.darksquare{
  background:#666161;
  color:white;
}

body{
  background:white
}

.darkb{
  background:#201c1c;
}

.main1{
  display:flex;
  justify-content: center;
}

.icont{
  font-size: 5rem;
  padding: 50px;
}

.fnt1{
  font-size: 2rem;
  padding:20px;
}

.fnt2{
  font-size: 2rem;
}


.fnt3{
  font-size: 3rem;
}

.buttons{
  display: flex;
  justify-content: space-between;
  margin-top: 100px;
}

.secondInfo{
  display:flex;
  justify-content: center;
}

.secondInfoch{
  justify-elemen: center;
}

.textinfo{
  
  text-align: center;
}

.toptop{
  margin-top: 30px;
}
.custom-select{
  -webkit-appearance: none;
  width:40%;
  appearance: none;
}

</style>



<template>
  <div class="container">
<div class="mt-5">prueba</div>
<div>
    <h5>Selecciona el estado</h5>
<select name="estados">


    <option v-for="estado in estados" :key="estado.id">{{estado}}</option>

</select>
<h5>Selecciona la ciudad</h5>

{{cities}}

<i class="wi size-5rem wi-rain" ></i>

</div>


{{pruebaclima}}
  </div>
</template>   




<script>
import Logo from '~/components/Logo.vue'
import axios from 'axios'
export default {
  data(){
    return{
        cities:'',
      pruebaclima: 'nada',
      estados:['Aguascalientes','Baja California','Baja California Sur','Campeche','Coahuila de Zaragoza','Colima','Chiapas','Chihuahua','Distrito Federal','Durango','Guanajuato','Guerrero','Hidalgo','Jalisco','México','Michoacán de Ocampo','Morelos','Nayarit','Nuevo León','Oaxaca','Puebla','Querétaro','Quintana Roo','San Luis Potosí','Sinaloa','Sonora','Tabasco','Tamaulipas','Tlaxcala','Veracruz de Ignacio de la Llave','Yucatán','Zacatecas'],
      cities:''

  }},
  created(){
    this.getwh()
    this.getcities()
  },
  methods:{
getwh() {
    
      const url = 'https://api.openweathermap.org/data/2.5/weather?q=london&appid=74809c652a768472e95f5d913143d783'
      const params={
          id:'2172797',
          appid:'74809c652a768472e95f5d913143d783'
      }
      axios
        .get(url,params)
        .then((response) => {
          this.pruebaclima = response.data
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
}}
</script>

<style lang="stylus" scoped>

</style>



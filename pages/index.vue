<template>
  <div class="container">
    <div>
        <button @click="getwh()">presiona</button>
      <p>{{pruebaclima}}</p>


    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import axios from 'axios'
export default {
  data(){
    return{
      prueba:'esto es 1111una prueba',
      pruebaclima: 'nada',
      pruebaclima1: ''
    }

  },
  created(){
    //this.getwh()
  },
  methods:{
getwh() {
      const url = 'api.openweathermap.org/data/2.5/weather?id=2172797&appid=74809c652a768472e95f5d913143d783'
      axios
        .get(url)
        .then((response) => {
          this.pruebaclima = response.data
        })
        .catch(() => {
          alert('error')
        })
    },
    
  },
  components: {
    Logo
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

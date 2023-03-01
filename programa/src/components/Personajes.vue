<script>
import axios from 'axios'


let API_URL = 'https://rickandmortyapi.com/api/character'

export default {

  data() {
    return {
      info: [],
      personajes: [],
      cont:2,
      search:"",
      id: 0,
      infoUno:[],
      personaje: [],
      mostrar: false,
    }
  },

  mounted() {
    axios.get(API_URL)
      .then((response) => {
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
  },

  methods: {
    //metodo para pagina anterior
    pagRe(num) {
      API_URL='https://rickandmortyapi.com/api/character/?page='+(num-1)
      console.log(API_URL)
      axios.get(API_URL)
      .then((response) => {
        console.log(response.config)
        this.info = response.data.info;
        console.log(this.info)
        this.personajes = response.data.results;
        
      })
      this.cont = this.cont-1
      
      
    },
    //metodo para pagina siguiente
    pagSig(num) {
      //url de consumo API
      API_URL='https://rickandmortyapi.com/api/character/?page='+num 
      //lo obtiene
      axios.get(API_URL)
      //
      .then((response) => {
        
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
      this.cont++
    },
    //informacion de un personaje
    InfoPer(id) {
      
      //url de consumo API
      API_URL='https://rickandmortyapi.com/api/character/'+id 
      console.log(API_URL)
      //lo obtiene
      axios.get(API_URL)
      //
      .then((response) => {
        console.log(response) //regresa datos de un solo personaje
        //contiene el array de cada personaje con sus datos
        this.infoUno = response.data;
        console.log(this.infoUno)
      })
      this.id++
      this.mostrar=true
      console.log(this.mostrar)
    }
  },
  computed: {
    //metodo para buscar
    filtrarBusqueda(){
      //busca en cada personaje
      return this.personajes.filter((personaje) => {
        //busca en el nombre del personaje
        return personaje.name.toLowerCase().includes(this.search.toLowerCase())
      })
    },

  },
}

</script>

<template class="flex mx-auto">

  <!--Total de personajes-->
  <h2 class="text-2xl my-10 text-center mx-5 sm:py-2">Hay un total de {{ info.count }} personajes en el programa de Rick & Morty</h2>

  
  <div class="grid grid-cols-2">
    <div>
      <!--Listado de cada 20 personajes o sea pagina-->
      <div class="text-2xl my-10 text-black mx-5 sm:py-2">
        <ul class=" ml-4 text-xl">
          <li v-for="p in personajes">
            <!--Llamando función obtener info personal por personaje-->
            <button @click="InfoPer(p.id)">{{ p.name }} id:{{ p.id }}</button>
            
          </li>
        </ul>
      </div>
    </div>
    
    <div>
      <!--carta de personaje-->
      <div v-if="mostrar">
        
        <div class="personaje">

          <img :src="infoUno.image" alt="">
          <div class="info-personaje">
            <h2> Nombre {{ infoUno.name}}</h2>
            <h4> Especie {{ infoUno.species}}</h4>
            <h4> Estado {{ infoUno.status}}</h4>

          </div>
          
        </div>
        
      </div>
    </div>
  </div>

  <!--Botones paginas-->
  <div class="mt-5">
      <!--Pagina anterior-->
      <button @click="pagRe(cont)" class=" ml-4 text-white bh-14 sm:h-10 px-7 font-semibold rounded-md bg-green-800 mb-8 justify-center shadow-xl hover:shadow-inner transition duration-500 ease-in-out  transform hover:-translate-x hover:scale-105" type="center">Anterior </button>
      <!--Contador-->
      <button @click="pag(cont)" class="p-5  ml-4" type="center">{{ cont }}</button>
      <!--Pagina anterior-->
      <button @click="pagSig(cont)" class=" ml-4 text-white bh-14 sm:h-10 px-7 font-semibold rounded-md bg-green-800 mb-8 justify-center shadow-xl hover:shadow-inner transition duration-500 ease-in-out  transform hover:-translate-x hover:scale-105" type="center">Siguiente </button>
  </div>
</template>
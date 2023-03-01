<script>
import axios from 'axios'


let API_URL = 'https://rickandmortyapi.com/api/character'

export default {

  data() {
    return {
      info: [],
      personajes: [],
      cont: 2,
      search: "",
      id: 0,
      infoUno: [],
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
      API_URL = 'https://rickandmortyapi.com/api/character/?page=' + (num - 1)
      console.log(API_URL)
      axios.get(API_URL)
        .then((response) => {
          console.log(response.config)
          this.info = response.data.info;
          console.log(this.info)
          this.personajes = response.data.results;

        })
      this.cont = this.cont - 1


    },
    //metodo para pagina siguiente
    pagSig(num) {
      //url de consumo API
      API_URL = 'https://rickandmortyapi.com/api/character/?page=' + num
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
      API_URL = 'https://rickandmortyapi.com/api/character/' + id
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
      this.mostrar = true
      console.log(this.mostrar)
    }
  },
  computed: {
    //metodo para buscar
    filtrarBusqueda() {
      //busca en cada personaje
      return this.personajes.filter((personaje) => {
        //busca en el nombre del personaje
        return personaje.name.toLowerCase().includes(this.search.toLowerCase())
      })
    },

  },
}

</script>
}

<template class="flex mx-auto">
  <!--Total de personajes-->
  <h2 class="text-2xl my-10 text-center mx-5 sm:py-2">Hay un total de {{ info.count }} personajes en el programa de Rick &
    Morty</h2>




  <div class="grid grid-cols-2 outline-2 outline-blue-700">
    <div>
      <form class="px-28">
        <label for="default-search" class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-white">Buscar</label>
        <div class="relative">
          <div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
            <svg aria-hidden="true" class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="none" stroke="currentColor"
              viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
            </svg>
          </div>
          <input type="search" id="default-search"
            class="block w-full p-4 pl-10 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="Personajes..." required>
          <button type="submit"
            class="text-white absolute right-2.5 bottom-2.5 bg-green-700 hover:bg-green-800 focus:ring-4 focus:outline-none focus:ring-green-300 font-medium rounded-lg text-sm px-4 py-2 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800">Search</button>
        </div>
      </form>
      <!--Listado de cada 20 personajes o sea pagina-->
      <div class=" px-2 text-2xl my-10 text-green-500 sm:py-2">
        <ul class=" ml-4 text-xl">
          <li v-for="p in personajes">
            <!--Llamando función obtener info personal por personaje-->
            <button @click="InfoPer(p.id)">{{ p.name }} id:{{ p.id }}</button>

          </li>
        </ul>
      </div>
    </div>

    <div class="text-center">
      <!--carta de personaje-->
      <div v-if="mostrar">

        <div class="personaje">
          <a href="#" class="relative block overflow-hidden rounded-lg border border-gray-100 p-4 sm:p-6 lg:p-8">
            <span class="absolute inset-x-0 bottom-0 h-2 bg-gradient-to-r from-green-800 "></span>

            <div class="sm:flex sm:justify-between sm:gap-4">
              <div>
                <h3 class="text-lg font-bold text-gray-900 sm:text-xl">
                  <strong> Nombre: </strong>{{ infoUno.name }}
                </h3>

                <p class="mt-1 text-xs font-medium text-gray-600">Rick y Morty</p>
              </div>


            </div>

            <img :src="infoUno.image" alt="" class=" py-3 h-25 w-35 rounded-lg object-cover shadow-sm " />

            <dl class="mt-6 flex gap-4 sm:gap-6">
              <div class="flex flex-col-reverse">
                <dt class="text-sm font-medium text-gray-600"> {{ infoUno.type }}</dt>
                <dd class="text-xs text-gray-500">Tipo</dd>
              </div>

              <div class="flex flex-col-reverse">
                <dt class="text-sm font-medium text-gray-600"> {{ infoUno.gender }}</dt>
                <dd class="text-xs text-gray-500">Generó</dd>
              </div>


              <div class="flex flex-col-reverse">
                <dt class="text-sm font-medium text-gray-600"> {{ infoUno.species }}</dt>
                <dd class="text-xs text-gray-500">Especie</dd>
              </div>

              <div class="flex flex-col-reverse">
                <dt class="text-sm font-medium text-gray-600"> {{ infoUno.status }}</dt>
                <dd class="text-xs text-gray-500">Estado</dd>
              </div>


            </dl>
          </a>

        </div>
      </div>
    </div>
  </div>



  <!--Botones paginas-->
  <div class="mt-5">
    <!--Pagina anterior-->
    <button @click="pagRe(cont)"
      class=" ml-4 text-white bh-14 sm:h-10 px-7 font-semibold rounded-md bg-green-800 mb-8 justify-center shadow-xl hover:shadow-inner transition duration-500 ease-in-out  transform hover:-translate-x hover:scale-105"
      type="center">Anterior </button>
    <!--Contador-->
    <button @click="pag(cont)" class="p-5  ml-4" type="center">{{ cont }}</button>
    <!--Pagina anterior-->
  <button @click="pagSig(cont)"
    class=" ml-4 text-white bh-14 sm:h-10 px-7 font-semibold rounded-md bg-green-800 mb-8 justify-center shadow-xl hover:shadow-inner transition duration-500 ease-in-out  transform hover:-translate-x hover:scale-105"
    type="center">Siguiente </button>
</div></template>
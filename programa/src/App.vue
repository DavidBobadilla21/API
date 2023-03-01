<script setup>
import { RouterLink, RouterView } from 'vue-router'

</script>

<template class="flex-col justify-center bg-green-500 w-full h-full p-2">
  <div class="w-full justify-items-center">



    <header class=" bg-green-700">
      <div class="wrapper">

        <nav class=" bg-green-700">
          <div class="grid grid-cols-3">
            <div></div>
            <div class=" bg-green-700">
              <img alt="Vue logo" class="logo" src="@/assets/Rick-And-Morty-Logo.webp" />
            </div>
            <div></div>
          </div>
        </nav>
      </div>
      <div class="grid grid-cols-5 items-center text-xxl text-white">
        <div></div>
        <div class=""> <button
            class=" bh-14 sm:h-10 px-7 font-semibold rounded-md bg-green-800 mb-8 justify-center shadow-xl hover:shadow-inner transition duration-500 ease-in-out  transform hover:-translate-x hover:scale-105">
            <RouterLink to="/">¿De que trata ?</RouterLink>
          </button></div>
        <div class="..."><button
            class="h-14 sm:h-10 px-7 font-semibold rounded-md bg-green-800  mb-8 justify-center shadow-xl hover:shadow-inner transition duration-500 ease-in-out  transform hover:-translate-x hover:scale-105">
            <RouterLink to="/personajes">Personajes</RouterLink>
          </button></div>
        <div class="..."><button
            class="h-14 sm:h-10 px-7 font-semibold rounded-md bg-green-800  mb-8 justify-center shadow-xl hover:shadow-inner transition duration-500 ease-in-out  transform hover:-translate-x hover:scale-105">
            <RouterLink to="/about" class="py-5">creditos</RouterLink>
          </button></div>
        <div></div>
      </div>
    </header>


    <RouterView />
  </div>
</template>
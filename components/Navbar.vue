<template>
  <div>
    <div>
      <div class="bg-hindu h-10"></div>

      <div class="p-3 font-bold text-xl text-center bg-white text-blue-600">Welcome to India</div>

      <div class="bg-muslim h-10"> </div>
    </div>
    <div class="flex gap-3 items-center p-3 bg-gray-600 text-white">
      <nuxt-link to="about">
        <div>About India </div>
      </nuxt-link>

      <nuxt-link to="history?asd=wert">        
        <div> History </div>
      </nuxt-link>

       <nuxt-link to="search">
        <div> Search </div>
      </nuxt-link>

    </div>
  </div>
</template>
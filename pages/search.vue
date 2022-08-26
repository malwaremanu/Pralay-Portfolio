<template>
  <div>
    <Navbar />
    <div>
      <div class="heading">Search Page</div>
    </div>
    <div class="p-6 mx-auto bg-gray-300">
      <div class="bg-white text-gray-900 p-3 m-3">
        <div class="p-3 lg:flex items-center gap-3" v-show="sbox">
          <input
            v-model="search_country"
            @keyup.enter="goandgetdata(search_country)"
            class="mb-2"
          />
          <button @click="goandgetdata(search_country)">Wiki Search</button>
        </div>

        <div v-show="!sbox" class="flex items-center justify-between gap-2 p-2">
          <button @click="sbox = true" v-show="!sbox">
            <svg
              class="w-4 h-4"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M15 19l-7-7 7-7"
              />
            </svg>
            Go Back
          </button>

          <div>
            <div class="text-center text-lg mb-3 px-6">
              <div class="text-3xl font-semibold text-center">{{ result.title }}</div>
              {{ result.description }}
            </div>
          </div>

          <div>
            <img :src="result.thumbnail ? result.thumbnail.source : ''" class="min-w-36 max-h-36" />
          </div>
        </div>

        <div class="p-3" v-show="!sbox" v-html="result.extract_html"></div>

        <div v-show="sbox">
          List of Popular Freedom Fighters
          <br />

          <div class="grid lg:grid-cols-5 md:grid-cols-3">
            <div v-for="r in revolutionaries" :key="r" class="p-1">
              <button @click="goandgetdata(r)">{{ r }}</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sbox: true,
      search_country: 'Bhutan',
      revolutionaries: [
        'Bhagat Singh',
        'Mahatama Gandhi',
        'Chandra Sekhar Azad',
        'Ram Prasad Bismil',
      ],
      result: {
        thumbnail: {
          source: '',
        },
      },
    }
  },
  methods: {
    async goandgetdata(x) {
      let response = await fetch(
        'https://en.wikipedia.org/api/rest_v1/page/summary/' + x,
        {
          method: 'GET',
        }
      )

      let data = await response.text()
      console.log(data)
      this.result = JSON.parse(data)
      this.sbox = false
    },
  },
}
</script>
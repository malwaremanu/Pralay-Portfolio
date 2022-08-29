<template>
  <div class="p-6">
    <div class="bg-green-50 rounded-md p-2">
      <div class="p-2">Text Input to Encrypt</div>
      <div class="p-2">
        <input type="text" v-model="ntxt.data.user" class="bg-green-200" />
        <input type="text" v-model="ntxt.data.pass" class="bg-green-200" />
      </div>
      <div class="px-3">Key : {{ secret }}</div>
      <div class="p-2">
        <button
          @click="enc(ntxt.data)"
          class="bg-green-400 hover:bg-green-500 text-white"
        >
          Submit
        </button>
      </div>
      {{ crpto }}
    </div>

    <hr />

    <div class="bg-green-50 rounded-md p-2">
      <div class="p-2">Text Input to Decrypt</div>
      <div class="p-2">
        <input type="text" v-model="txt.data" class="bg-green-200 w-full" />
      </div>
      <div class="px-3">Key : {{ secret }}</div>
      <div class="p-2">
        <button
          @click="dec(txt.data)"
          class="bg-green-400 hover:bg-green-500 text-white"
        >
          Submit
        </button>
      </div>
      {{ orig }}
    </div>
  </div>
</template>
<script>
var CryptoJS = require('crypto-js')

export default {
  data() {
    return {
      ntxt: {
        data: {
          user : "manu",
          pass : "password"
        },
      },
      txt: {
        data: 'g4Wc4MXN8qB1PPbngFWQav3Vp9+Pfj0EiuA0s4S8MTnkoiTkXgWiTwpGUSmL0Pfa',
      },
      //secret: "dRgUkXp2s5v8y/B?",
      secret: CryptoJS.enc.Utf8.parse("PoncU&*()/12345aPoncU&*()/12345a"),
      crpto: '',
      orig: '',
      
    }
  },
  methods: {
    enc(x) {     
      var encrypted = CryptoJS.AES.encrypt(JSON.stringify(x), this.secret, {
        mode: CryptoJS.mode.ECB,
      })
      encrypted = encrypted.toString()      
      this.txt.data = encrypted
      return encrypted
    },
    
    dec(x) {
      var decrypted = CryptoJS.AES.decrypt(x, this.secret, {
        mode: CryptoJS.mode.ECB,
      })
      decrypted = decrypted.toString(CryptoJS.enc.Utf8)      
      this.orig = decrypted
      return decrypted
    },
  },
}
</script>
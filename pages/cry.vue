<template>
  <div class="p-6">
    <div class="bg-green-50 rounded-md p-2">
      <div class="p-2">Text Input to Encrypt </div>
      <div class="p-2">
        <input type="text" v-model="txt" class="bg-green-200"/>
      </div>
      <div class="px-3">
        Key : {{ secret }}
      </div>
      <div class="p-2">
        <button @click="enc" class="bg-green-400 hover:bg-green-500 text-white">Submit</button>
      </div>
      {{ crpto }}
    </div>

    <hr />    

    <div class="bg-green-50 rounded-md p-2">
      <div class="p-2">Text Input to Decrypt </div>
      <div class="p-2">
        <input type="text" v-model="txt" class="bg-green-200"/>
      </div>
      <div class="px-3">
        Key : {{ secret }}
      </div>
      <div class="p-2">
        <button @click="dec" class="bg-green-400 hover:bg-green-500 text-white">Submit</button>
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
      txt: "this is something",
      secret: "v8y/B?E(H+MbQeShVmYq3t6w9z$C&F)J",
      crpto : '',
      orig : ''
    }
  },
  methods: {
    enc() {
      // Encrypt
      var ciphertext = CryptoJS.AES.encrypt(this.txt, this.secret).toString()
      console.log('Cipher Text', ciphertext)
      this.crpto = ciphertext
      console.log('Decoded Text', ciphertext) // 'my message'
    },

    dec() {      
      // Decrypt
      var bytes = CryptoJS.AES.decrypt(this.crpto, this.secret)
      var originalText = bytes.toString(CryptoJS.enc.Utf8)
      this.orig = originalText
      console.log('Decoded Text', originalText) // 'my message'
    },
  },
}
</script>
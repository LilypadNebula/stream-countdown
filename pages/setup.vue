<template>
  <div class="flex flex-col h-screen">
    <p class="p-16 text-3xl">
      Here you can choose your options for the countdown. Choose from the options on the left, and see what they look like
      on the right. When you've got something you like, you can copy the link yourself, or click the button to copy it, and you're good! Copy it into your
      streaming software as a Browser Source, or whatever other thing you need a simple timer for.
    </p>
    <div class="flex justify-center">
      <div class="flex flex-wrap">
        <div
          class="flex flex-col justify-center items-center border border-black rounded shadow m-2 p-4 w-2/5"
        >
          <p class="text-2xl mb-2">Timer Length</p>
          <input
            type="number"
            min="1"
            v-model="length"
            class="text-2xl p-4 text-center border border-black rounded focus:outline-none"
          >
        </div>
        <div
          class="flex flex-col justify-center items-center border border-black rounded shadow m-2 p-4 w-2/5"
        >
          <p class="text-2xl mb-2">Font Options</p>
          <div class="flex flex-col">
            <div class="m-1">
              <input type="radio" name="font" id="defaultFont" value="standard" v-model="font">
              <label class="text-4xl" for="defaultFont" :style="{fontFamily:'standard'}">Default</label>
            </div>
            <div class="m-1">
              <input type="radio" name="font" id="spookyFont" value="spooky" v-model="font">
              <label class="text-4xl" for="spookyFont" :style="{fontFamily:'spooky'}">Spooky</label>
            </div>
            <div class="m-1">
              <input type="radio" name="font" id="digiFont" value="digi" v-model="font">
              <label class="text-4xl" for="digiFont" :style="{fontFamily:'digi'}">Digi</label>
            </div>
            <div class="m-1">
              <input type="radio" name="font" id="fancyFont" value="fancy" v-model="font">
              <label class="text-4xl" for="fancyFont" :style="{fontFamily:'fancy'}">Fancy</label>
            </div>
          </div>
        </div>
        <div
          class="flex flex-col justify-center items-center border border-black rounded shadow m-2 p-4 w-2/5"
        >
          <p class="text-2xl mb-2">Color</p>
          <verte display="vertical-widget" model="hex" v-model="color"></verte>
        </div>
        <div
          class="flex flex-col justify-center items-center border border-black rounded shadow m-2 p-4 w-2/5"
        >
          <p class="text-2xl mb-2">Message</p>
          <input
            type="text"
            v-model="message"
            class="text-2xl p-4 text-center border border-black rounded focus:outline-none"
          >
        </div>
      </div>
      <div class="flex flex-col justify-center break-words">
        <p class="text-center text-5xl" :style="{fontFamily:font,color}">{{length}}:00</p>
        <p class="text-center text-5xl max-w-md" :style="{fontFamily:font,color}">{{message}}</p>
        <p class="text-center text-4xl mt-8 max-w-md">{{customURL}}</p>
        <button
          class="p-8 text-2xl rounded bg-blue-dark text-white w-64 mx-auto"
          @click="copyLink"
        >Copy Link</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      length: 4,
      font: 'standard',
      color: '#000000',
      message: 'Soon!'
    }
  },
  computed: {
    customURL() {
      let suffix = ''
      if (this.length != 4) suffix += `length=${this.length}&`
      if (this.font != 'standard') suffix += `font=${this.font}&`
      if (this.color != '#000000')
        suffix += `color=%23${this.color.substring(1)}&`
      if (this.message != 'Soon!')
        suffix += `message=${encodeURI(this.message)}&`
      if (suffix.length > 0)
        return `${process.env.baseURL}?${suffix}`.slice(0, -1)
      else return process.env.baseURL
    }
  },
  methods: {
    copyLink() {
      navigator.clipboard.writeText(this.customURL)
      alert('Your URL has been copied!')
    }
  }
}
</script>

<template>
  <div class="flex flex-col">
    <div class="flex justify-between">
      <div
        class="flex flex-col justify-center items-center border border-black rounded shadow m-16 p-8"
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
        class="flex flex-col justify-center items-center border border-black rounded shadow m-16 p-8"
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
        class="flex flex-col justify-center items-center border border-black rounded shadow m-16 p-8"
      >
        <p class="text-2xl mb-2">Color</p>
        <verte display="vertical-widget" model="hex" v-model="color"></verte>
      </div>
      <div
        class="flex flex-col justify-center items-center border border-black rounded shadow m-16 p-8"
      >
        <p class="text-2xl mb-2">Message</p>
        <input
          type="text"
          v-model="message"
          class="text-2xl p-4 text-center border border-black rounded focus:outline-none"
        >
      </div>
    </div>
    <p class="text-center text-5xl" :style="{fontFamily:font,color}">{{length}}:00</p>
    <p class="text-center text-5xl" :style="{fontFamily:font,color}">{{message}}</p>
    <p class="text-center text-4xl mt-8">{{customURL}}</p>
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
  }
}
</script>

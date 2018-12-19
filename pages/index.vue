<template>
  <p
    :style="{fontFamily:font,fontSize:'20em',color:color}"
    class="text-center break-words"
  >{{display}}</p>
</template>

<script>
const moment = require('moment')

export default {
  data() {
    return {
      length: null,
      font: null,
      color: null,
      message: null,
      timer: null
    }
  },
  beforeMount() {
    const myURL = new URL(window.location.href)
    this.length = myURL.searchParams.get('length') || 4
    if (this.length < 1) this.length = 1
    switch (myURL.searchParams.get('font')) {
      case 'spooky':
        this.font = 'spooky'
        break
      case 'digi':
        this.font = 'digi'
        break
      case 'fancy':
        this.font = 'fancy'
        break
      default:
        this.font = 'standard'
    }
    this.color = myURL.searchParams.get('color') || '#000000'
    this.message = myURL.searchParams.get('message') || 'Soon!'
    this.timer = moment.duration({ minutes: this.length })
    setInterval(() => this.timer.subtract(1000), 1000)
  },
  computed: {
    display() {
      if (!this.timer) return ''
      else if (this.timer.asSeconds() > 0)
        return `${this.timer.minutes()}:${this.timer
          .seconds()
          .toString()
          .padStart(2, '0')}`
      else return this.message
    }
  }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>

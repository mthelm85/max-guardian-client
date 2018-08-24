<template lang="html">
  <div class="container">
    <div class="row align-items-center">
      <div class="col d-flex justify-content-center text-center">
        <div class="color rounded d-flex align-items-center" :style="{ backgroundColor: color }">
          <span class="mx-auto display-1 text-white">{{ rssi }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Howl } from 'howler'
export default {
  data () {
    return {
      rssi: null
    }
  },

  computed: {
    color () {
      let n = this.rssi
      if (n <= 65) {
        return 'red'
      } else if (n > 65 && n <= 85) {
        return 'orange'
      } else {
        return 'green'
      }
    }
  },

  sockets: {
    connect () {
      alert('Connected to socket...')
    },
    forwardRssi (rssi) {
      this.rssi = rssi
    }
  },

  watch: {
    rssi () {
      if (this.rssi <= 65) {
        const alarm = new Howl({
          src: ['/static/alarm.wav']
        })
        if (alarm.playing()) {
          return
        } else {
          alarm.play()
        }
      }
    }
  }

}
</script>

<style lang="css">
.color {
  height: 400px;
  width: 400px;
}
.row {
  height: 100vh;
}
</style>

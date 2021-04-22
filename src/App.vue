<template>
  <v-app>
    <v-app-bar
      app
      color="deep-orange darken-2"
      elevation="0"
      dark
    >
      <div class="heading fw-100 flex f-jcc f-aic">
        <span>Beeper</span>
      </div>
    </v-app-bar>
    

    <v-main class="brown darken-2 text-center f-aic">
      <!-- <div class="mixer"></div> -->
      <v-container class="white--text">
        <div class="empty-space" @click="minutes=minutes-1"></div>
        <span @click="setTime"
              class="big-heading"
              :style="{color: getColor}"
        >
        {{minutes}}
        </span>
        <div class="empty-space" @click="minutes=minutes+1"></div>
      </v-container>
    </v-main>
    <v-footer class="deep-orange darken-4" padless>
      <v-col
      class="text-center white--text"
      >
        © Prakhar Chaurasiya
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>


export default {
  name: 'App',

  components: {
    
  },

  data: () => ({
    minutes: 5,
    status: false,
    beep: new Audio(require('./assets/beep.mp3'))
  }),
  computed: {
    getMinutes() {
      if (this.minutes < 1) {
        return 1
      } else if (this.minutes > 60) {
        return 60
      } else {
        return this.minutes
      }
    },
    getColor() {
      if(this.status) {
        return 'white'
      } else {
        return '#5D4037'
      }
    }
  },
  mounted() {
    setInterval(() => {
      if(this.status) {
        this.beep.play()
      }
    }, this.getMinutes()*1000)
  },
  methods: {
    setTime() {
      this.status = !this.status
      console.log(this.status)
      this.beep.play()
    }
  }
};
</script>
<style>
* {
  font-family: 'Roboto' ,'Times New Roman', Times, serif;
}
.heading {
  font-size: 2em;
}
.mixer {
  height: 10px;
  background: linear-gradient(#E64A19,#5D4037)
}
.big-heading {
  font-size: 20em;
  font-weight: bold;
  cursor: pointer;
}
.empty-space {
  background: #5D4037;
  height: 100px;
}
</style>

<template>
  <h1>Comestible Digestibles swag af soundboard!!!!!!!!</h1>
  <div class="flex-soundboard-container">
    <div class="flex-soundboard">
      <div v-for="sound in getSoundFiles()" :key="sound" class="sound" @click="playSound(sound)">
        <p>{{ sound }}</p>
      </div>
    </div>
    <div>
      <button @click="stopAllSounds">Stop All Sounds</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  computed: {
    getSoundFiles() {
      return function() {
        return require.context('../public/sounds', false).keys()
      }
    }
  },
  methods: {
    playSound(sound) {
      sound = sound.replace('./', '')
      const audio = new Audio("/sounds/" + sound)
      audio.play()
      this.sounds.push(audio)
    },
    stopAllSounds() {
      this.sounds.forEach(audio => {
        audio.pause()
      })
      this.sounds = []
    }
  },
  data() {
    return {
      sounds: []
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.flex-soundboard-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.flex-soundboard {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: 80%;
}

.sound {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;
  margin: 10px;
  background-color: #f2f2f2;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.3s ease;
  border: 1px solid #000;
}
</style>

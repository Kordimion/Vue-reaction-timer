<template>
  <h1>Reaction timer</h1>
  <p>Click the box as soon as possible</p>

    <GameBox 
      v-if="isGameStarted" 
      @clickedEarly="handleEarlyClick" 
      @clickedOnTime="handleClickOnTime"
    />

  <Results v-if="!isGameStarted" @click="isGameStarted = true">
    <h3 v-if="results === null">Click me to start the game</h3>
    <div v-if="results"> 
     <h3>{{results.message}} </h3> 
     <p> try again </p>
    </div>

  </Results>
</template>

<script>
  import GameBox from './components/GameBox.vue'
  import Results from './components/Results.vue'

export default {
  name: 'App',
  components: {GameBox,Results},
  data() {
    return {
      isGameStarted: false,
      results: null
    }
  },
  methods: {
    handleEarlyClick() {
      console.log("clicked early")
      this.isGameStarted = false;
      this.results = {
        message: "You clicked too early"
      }
    },
    handleClickOnTime(time) {
      console.log("you clicked on time")
      console.log("your result is ", time)
      this.isGameStarted = false;
      this.results = {
        message: "Your reaction time: " + time
      }
    }
  }
}
</script>

<style>
#app {
  text-align: center;
}

.box {
  width: 45rem;
  height: 20rem;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 1rem;
  background-color: #059669;
  font-size: 2.5rem;
  color: white;
  padding: 1rem;
  margin-top: 1rem;
}
</style>

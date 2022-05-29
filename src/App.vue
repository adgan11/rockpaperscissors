<template>
  <rpsAI />
</template>

<script>
import rpsAI from './components/rpsAI.vue'

export default {
  name: 'App',
  components: {
    rpsAI,
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
</style>


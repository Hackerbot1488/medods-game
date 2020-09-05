<template>
	<div id="app">
		<Game />
	</div>
</template>

<script>
import Game from "./components/Game.vue";

export default {
	meta: {
		title: "Simon Says",
	},
	name: "App",
	components: {
		Game,
	},
};
</script>

<style lang="sass">
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap')
*
  box-sizing: border-box
body
  margin: 0
  padding: 0
#app
  font-family: 'Poppins', sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  /** overflow: hidden **/
  /** background-color: #263238 **/
  /** background-color: #9395ff **/
  /** background-color: #d2c2fd **/
  background-color: #aff1d1
  color: #b71c1c
  min-height: 100vh
  padding-top: 50px
  padding-bottom: 50px
  display: flex
  align-items: center
</style>

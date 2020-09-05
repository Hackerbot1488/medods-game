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
@font-face 
  font-family: "Poppins"
  src: url("/fonts/Poppins/Poppins-Regular.eot")
  src: url("/fonts/Poppins/Poppins-Regular.ttf") format("opentype"),
		url("/fonts/Poppins/Poppins-Regular.woff2") format("woff2"),
		url("/fonts/Poppins/Poppins-Regular.svg") format("svg")
  font-style: normal
  font-weight: normal

@font-face
  font-family: "Poppins"
  src: url("/fonts/Poppins/Poppins-Bold.eot")
  src: url("/fonts/Poppins/Poppins-Bold.ttf") format("opentype"),
		url("/fonts/Poppins/Poppins-Bold.woff2") format("woff2"),
		url("/fonts/Poppins/Poppins-Bold.svg") format("svg")
  font-style: normal
  font-weight: bold

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

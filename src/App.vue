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
*
  box-sizing: border-box
body
  margin: 0
  padding: 0
  min-height: 100vh
#app
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  /** background-color: #263238 **/
  /** background-color: #9395ff **/
  background-color: black
  min-height: 100vh
  display: flex
  align-items: center
</style>

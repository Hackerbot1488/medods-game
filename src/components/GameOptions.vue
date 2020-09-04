<template>
	<div class="game-options">
		<div class="game-options__container">
			<h2 class="game-options__title">Round: {{round}}</h2>
			<button class="game-options__button" @click="() => !game && $emit('start-game')">Start</button>
		</div>
		<div class="game-options__container">
			<p v-if="lost" class="game-options__message">Sorry, you lost after {{round-1}} rounds.</p>
		</div>
		<div class="game-options__container">
			<h2 class="game-options__title">Complexity:</h2>
			<div class="game-options__complexity">
				<div class="wrap-radio">
					<input type="radio" name="complexity" id="easy" value="1500" v-model="delay" />
					<label for="easy">Easy</label>
				</div>
				<div class="wrap-radio">
					<input type="radio" name="complexity" id="medium" value="1000" v-model="delay" />
					<label for="medium">Medium</label>
				</div>
				<div class="wrap-radio">
					<input type="radio" name="complexity" id="hard" value="400" v-model="delay" />
					<label for="hard">Hard</label>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
export default {
	name: "GameOptions",
	props: {
		round: {
			type: Number,
			default: 0,
		},
		lost: {
			type: Boolean,
			default: false,
		},
		game: {
			type: Boolean,
			default: false,
		},
	},
	data() {
		return {
			delay: 1000,
		};
	},
	watch: {
		delay() {
			!this.game && this.$emit("delayChange", this.delay);
		},
	},
};
</script>
<style lang="sass" scoped>
.game-options
  display: flex
  flex-direction: column
  color: white
  margin: 0 auto
  &__container
    display: flex
    flex-direction: column
    width: 150px
  &__button
    padding: 10px 20px
    font-size: 20px
    border: none
    outline: none
    border-radius: 10px
    background-color: #ffcdd2
    color: white
    cursor: pointer
  &__complexity
    display: flex
    flex-direction: column
    label
      font-size: 20px
      font-family: Arial, Helvetica, sans-serif
      margin-left: 15px
    input
      margin: 0
    .wrap-radio
      margin-top: 5px
      margin-bottom: 5px
      display: flex
      align-items: center
  &__container
    flex: 1
  &__title
    font-size: 25px
    font-family: Arial, Helvetica, sans-serif
    text-align: left
  
</style>
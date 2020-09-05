<template>
	<div class="game-options">
		<div class="game-options__container">
			<h2 class="game-options__title">Round: {{round}}</h2>
			<button class="game-options__button" @click="() => !game && $emit('start-game')">Start</button>
		</div>
		<div class="game-options__container">
			<p v-if="lost" class="game-options__message">Sorry, you lost on {{lastRound}} round.</p>
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
		lastRound: {
			type: Number,
			default: 0,
		},
	},
	data() {
		return {
			delay: 1000,
		};
	},
	watch: {
		delay() {
			console.log(this.delay);
			!this.game && this.$emit("delayChange", this.delay);
		},
	},
};
</script>
<style lang="sass" scoped>
.game-options
	display: flex
	flex-direction: column
	margin: 0 auto
	&__container
		display: flex
		flex-direction: column
		width: 300px
	&__button
		padding: 10px 20px
		font-size: 20px
		max-width: 120px
		border: none
		outline: none
		border-radius: 10px
		color: #aff1d1
		/** background-color: #FFCCBC **/
		background-color: #E53935
		cursor: pointer
		transition: .5s
		&:hover
			/** background-color: #FF5722 **/
			background-color: #B71C1C
	&__complexity
		display: flex
		flex-direction: column
		label
			font-size: 20px
			margin-left: 15px
		input
			margin: 0
		.wrap-radio
			margin-top: 5px
			margin-bottom: 5px
			display: flex
			align-items: center
	&__container
		min-height: 54px
	&__title
		font-size: 25px
		margin: 0 0 5px
		font-weight: bold
		text-align: left
	&__message
		font-size: 15px
		text-align: left
@media (max-width: 720px)
	.game-options
		&__container
			width: 270px
			margin-left: 30px
</style>
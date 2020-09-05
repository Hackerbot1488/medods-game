<template>
	<div class="game">
		<div class="game__container">
			<GameBoard
				:delay="delay"
				:start="isPlaying"
				:colors="colorsForRound"
				@nextRound="onNextRound"
				@endGame="endGame"
				:key="keyComp"
			/>
		</div>
		<div class="game__container">
			<GameOptions
				:lost="lost"
				:round="round"
				:key="keyOpt"
				:game="isPlaying"
				:lastRound="lastRound"
				:lightDelay="String(delay)"
				@start-game="startGame"
				@delayChange="(value) => delay = value"
			/>
		</div>
	</div>
</template>

<script>
import GameBoard from "@/components/GameBoard.vue";
import GameOptions from "@/components/GameOptions.vue";
export default {
	name: "Game",
	data() {
		return {
			colors: ["blue", "red", "orange", "green"],
			colorsForRound: [],
			round: 0,
			delay: 1000,
			isPlaying: false,
			keyComp: 454848,
			keyOpt: 735735,
			timeouts: [],
			lost: false,
			lastRound: 0,
		};
	},
	methods: {
		addColor() {
			this.colorsForRound.push(this.colors[Math.floor(Math.random() * 4)]);
		},
		onNextRound() {
			this.timeouts.push(
				setTimeout(() => {
					this.addColor();
					this.round++;
					this.updateBoard();
					this.updateOptions();
				}, 500)
			);
		},
		endGame() {
			this.colorsForRound = [];
			this.lost = true;
			this.lastRound = this.round;
			this.round = 0;
			this.updateOptions();
			this.isPlaying = false;
			this.updateBoard();
			this.clearTimeouts();
		},
		startGame() {
			this.addColor();
			this.round = 1;
			this.isPlaying = true;
			this.lost = false;
			this.updateBoard();
			this.updateOptions();
		},
		updateBoard() {
			this.keyComp++;
		},
		updateOptions() {
			this.keyOpt++;
		},
		clearTimeouts() {
			this.timeouts.forEach((t) => clearTimeout(t));
			this.timeouts = [];
		},
	},
	components: {
		GameBoard,
		GameOptions,
	},
	mounted() {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="sass">
.game
	margin: 0 auto
	max-width: 720px
	display: flex
	&__container
		width: 300px
		align-items: center
		margin-left: 60px

@media (max-width: 720px)
	.game
		width: 100%
		flex-direction: column
		margin: 0
		&__container
			margin: 0 auto
		&__container:last-child
			margin-top: 30px
</style>

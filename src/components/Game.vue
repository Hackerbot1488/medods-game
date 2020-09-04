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
			delay: 400,
			isPlaying: false,
			keyComp: 454848,
			keyOpt: 735735,
			timeouts: [],
			lost: false,
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
			console.log("end game");
			this.colorsForRound = [];
			this.updateOptions();
			this.round = 0;
			this.lost = true;
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
	max-width: 1000px
	display: flex
	flex: 1
	&__container
		flex: 1
		align-items: center
</style>

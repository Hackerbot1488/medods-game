<template>
	<div class="game-board" data-role="board" @click="(e) => !blocked && onClick(e)">
		<button
			:class="['game-board__button', 'game-board__button_blue',  !!delay ? `t-${delay}` : '']"
			data-color="blue"
			ref="blue"
		></button>
		<button
			:class="['game-board__button', 'game-board__button_red',  !!delay ? `t-${delay}` : '']"
			data-color="red"
			ref="red"
		></button>
		<button
			:class="['game-board__button', 'game-board__button_green',  !!delay ? `t-${delay}` : '']"
			data-color="green"
			ref="green"
		></button>
		<button
			:class="['game-board__button', 'game-board__button_orange',  !!delay ? `t-${delay}` : '']"
			data-color="orange"
			ref="orange"
		></button>
	</div>
</template>
<script>
export default {
	name: "GameBoard",
	props: {
		colors: {
			type: Array,
			default: () => [],
		},
		delay: {
			type: Number,
			default: 1000,
		},
		start: {
			type: Boolean,
			default: false,
		},
	},
	data() {
		return {
			iteratorInterval: 0,
			iteratorTimeout: 0,
			blocked: true,
			interval: null,
			previous: null,
			timeouts: [],
		};
	},
	methods: {
		onClick(e) {
			if (!e.target.dataset.role) {
				e.target.classList.add("clicked");
				this.timeouts.push(
					setTimeout(() => {
						e.target.classList.remove("clicked");
						if (e.target.dataset.color === this.colors[this.iteratorTimeout]) {
							this.iteratorTimeout++;
						} else {
							this.endRound();
						}
						this.iteratorTimeout === this.colors.length && this.nextRound();
					}, 500)
				);
			}
		},
		startRaund() {
			this.interval = setInterval(() => {
				this.$refs[this.previous]?.classList.remove("clicked");
				if (this.iteratorInterval < this.colors.length) {
					this.$refs[this.colors[this.iteratorInterval]].classList.add(
						"clicked"
					);
					if (
						this.colors[this.iteratorInterval] ===
						this.colors[this.iteratorInterval + 1]
					) {
						this.timeouts.push(
							setTimeout(
								(color) => {
									this.$refs[color].classList.remove("clicked");
								},
								this.delay / 2,
								this.colors[this.iteratorInterval]
							)
						);
					}
					this.previous = this.colors[this.iteratorInterval];
					this.iteratorInterval++;
				} else {
					this.previous = null;
					this.iteratorInterval = 0;
					this.blocked = false;
					clearInterval(this.interval);
				}
			}, this.delay);
		},
		clearTimeouts() {
			this.timeouts.forEach((t) => clearTimeout(t));
			this.timeouts = [];
		},
		endRound() {
			this.blocked = true;
			this.iteratorTimeout = 0;
			this.clearTimeouts();
			this.$emit("endGame");
		},
		nextRound() {
			this.blocked = true;
			this.iteratorTimeout = 0;
			this.clearTimeouts();
			this.$emit("nextRound");
		},
	},
	mounted() {
		this.start && this.startRaund();
	},
};
</script>
<style lang="sass" scoped>
$blue_common: #81d4fa
$blue_active: #01579b
$red-common: #ffcdd2
$red_active: #b71c1c
$green-common: #defabb
$green_active: #008b00
$orange-common: #FFE0B2
$orange_active: #E65100
@keyframes blueToActive
	0%
		background-color: $blue_active
	75%
		background-color: $blue_common
@keyframes orangeToActive
	0%
		background-color: $orange_active
	75%
		background-color: $orange_common
@keyframes redToActive
	0%
		background-color: $red_active
	75%
		background-color: $red_common
@keyframes greenToActive
	0%
		background-color: $green_active
	75%
		background-color: $green_common

.game-board
	width: 300px
	height: 300px
	margin: 0 auto
	border: 4px solid white
	border-radius: 50%
	background-color: white
	position: relative
	&__button
		width: calc(100%/2)
		height: calc(100%/2)
		border: none
		position: absolute
		outline: none
		cursor: pointer
		&.t-400
			transition: 0.4s
		&.t-1000
			transition: 1s
		&.t-1500
			transition: 1.5s
		&_blue
			border: 2px solid white
			border-right: none
			border-bottom: none
			border-top-left-radius: 100%
			border-color: $blue_common
			background-color: $blue_common
			top: 0
			left: 0
			&.clicked
				animation: blueToActive 1s ease-in
				animation-iteration-count: 1
			&:hover
				border-color: $blue_active
		&_red
			border: 2px solid white
			border-left: none
			border-bottom: none
			border-top-right-radius: 100%
			border-color: $red_common
			background-color: $red_common
			right: 0
			top: 0
			&.clicked
				animation: redToActive 1s ease-in
				animation-iteration-count: 1
			&:hover
				border-color: $red_active
		&_green
			border: 2px solid white
			border-left: none
			border-top: none
			border-bottom-right-radius: 100%
			border-color: $green_common
			background-color: $green_common
			right: 0
			bottom: 0
			&.clicked
				animation: greenToActive 1s ease-in
				animation-iteration-count: 1
			&:hover
				border-color: $green_active
		&_orange
			border: 2px solid white
			border-right: none
			border-top: none
			border-bottom-left-radius: 100%
			border-color: $orange_common
			background-color: $orange_common
			left: 0
			bottom: 0
			&.clicked
				animation: orangeToActive 1s ease-in
				animation-iteration-count: 1
			&:hover
				border-color: $orange_active
</style>

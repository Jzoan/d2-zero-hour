<template>
	<v-container>
		<v-layout text-xs-center wrap class="no-padding-after">
			<v-flex xs12 offset-xl2 xl8 class="no-padding-after">
				<v-layout text-xs-center wrap class="no-padding-after">
					<v-flex xs12 offset-sm2 sm8 offset-md0 md4>
						<NumberPad
							:element="element"
							label="Console 1 - Left"
							:resetToggle="resetToggle"
							@change="val => { this.num1 = val; solveCombination(); }"
						/>
					</v-flex>
					<v-flex xs12 offset-sm2 sm8 offset-md0 md4>
						<NumberPad
							:element="element"
							label="Console 1 - Right"
							:resetToggle="resetToggle"
							@change="val => { this.num2 = val; solveCombination() }"
						/>
					</v-flex>
					<v-flex xs12 offset-sm2 sm8 offset-md0 md4>
						<NumberPad
							:element="element"
							:label="'Console 3 - Left'"
							:resetToggle="resetToggle"
							@change="val => { this.num3 = val; solveCombination(); }"
						/>
					</v-flex>
					<v-flex xs12 offset-md1 md5 offset-xl0 xl6>
						<HallView id="hall" :room="room" :element="element" :resetToggle="resetToggle"/>
					</v-flex>
					<v-flex xs12 md5 xl6>
						<RoomView id="room" :terminal="terminal" :element="element" :resetToggle="resetToggle"/>
					</v-flex>
					<v-flex offset-xs2 xs8 offset-sm4 sm4 class="no-padding-after">
						<v-btn block @click="reset();">Reset</v-btn>
					</v-flex>
				</v-layout>
			</v-flex>
		</v-layout>
	</v-container>
</template>

<script>
	import NumberPad from "./NumberPad";
	import HallView from "./HallView";
	import RoomView from "./RoomView";
	import CombinationsDB from "./CombinationsDB";

	export default {
		name: "PuzzleSolver",
		components: {
			CombinationsDB,
			HallView,
			NumberPad,
			RoomView
		},
		data: () => ({
			num1: null,
			num2: null,
			num3: null,
			resetToggle: 0,
			room: null,
			terminal: null
		}),
		props: {
			element: String
		},
		watch: {
			element: function() {
				this.reset();
			}
		},
		methods: {
			reset: function() {
				this.resetToggle = 1 - this.resetToggle;
				this.room = null;
				this.terminal = null;
				this.$vuetify.goTo(-9999, {
					duration: 750
				});
			},
			solveCombination: function() {
				// determine known matching combinations
				let results = CombinationsDB.combinations[this.element].filter(a => {
					return (
						(!this.num1 || (this.num1 && a.console1.left === this.num1)) &&
						(!this.num2 || (this.num2 && a.console1.right === this.num2)) &&
						(!this.num3 || (this.num3 && a.console3.left === this.num3))
					);
				});

				console.log("results", results);

				// display result if a single combination matches
				if (results.length === 1) {
					this.room = results[0].target.room;
					this.terminal = results[0].target.terminal;
					this.$vuetify.goTo("#hall", {
						duration: 750
					});
				} else {
					this.room = null;
					this.terminal = null;
				}
			}
		}
	};
</script>

<style lang="scss" scoped>
	.no-padding-after {
		padding-bottom: 0 !important;
	}
</style>

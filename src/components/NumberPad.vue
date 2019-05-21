<template>
	<v-btn-toggle class="number-pad" v-model="value" @change="updateInput">
		<v-layout text-xs-center wrap>
			<v-flex xs12>
				<h2 class="title">{{ label }}</h2>
			</v-flex>
			<v-flex xs3 v-for="(option, i) in 12" :key="i">
				<v-btn block :class="`theme--${element}`" :value="option">{{ option }}</v-btn>
			</v-flex>
		</v-layout>
	</v-btn-toggle>
</template>

<script>
	export default {
		name: "NumberPad",
		data: () => ({
			value: null
		}),
		props: {
			element: String,
			label: String,
			resetToggle: Number
		},
		methods: {
			updateInput() {
				this.$emit("change", this.value);
			},
			reset() {
				this.value = null;
				this.updateInput();
			}
		},
		watch: {
			element: function() {
				this.reset();
			},
			resetToggle: function() {
				this.reset();
			}
		}
	};
</script>

<!-- Inheritable Styles -->
<style lang="scss">
	.flex {
		padding: 0px 15px 15px 15px;
	}

	.theme--arc {
		.number-pad {
			.v-btn--active,
			.v-btn--active::before,
			.v-btn:hover::before,
			.v-btn:focus::before {
				background-color: #008f9b !important;
			}
		}
	}

	.theme--solar {
		.number-pad {
			.v-btn--active,
			.v-btn--active::before,
			.v-btn:hover::before,
			.v-btn:focus::before {
				background-color: #a23f00 !important;
			}
		}
	}

	.theme--void {
		.number-pad {
			.v-btn--active,
			.v-btn--active::before,
			.v-btn:hover::before,
			.v-btn:focus::before {
				background-color: #4d1a84 !important;
			}
		}
	}

	.title {
		margin-bottom: 10px;
	}

	.number-pad {
		width: 100%;
		padding: 15px 5px;

		.flex {
			padding: 5px;
		}

		.v-btn--block {
			width: 100%;
			height: 50px;
			font-size: 17px;
			color: #9c9c9c !important;
		}
	}

	// mobile tweaks
	@media screen and (max-width: 1023px) {
		.number-pad {
			padding: 5px;
			height: calc((100vh - 115px) / 3);

			.flex {
				padding: 3px;
			}

			.v-btn--block {
				height: 100%;
			}
		}

		.title {
			margin-bottom: 0;
			font-size: 17px !important;
		}
	}
</style>

<template>
	<div class="room-container">
		<div class="terminal" v-for="(option, i) in 7" :key="i" :class="{ active: option == terminal }">
			<span class="name">{{ option }}</span>
		</div>
		<div class="border top"></div>
		<div class="border left"></div>
		<div class="border right"></div>
		<div class="border bottom-left"></div>
		<div class="border bottom-right"></div>
	</div>
</template>

<script>
	export default {
		name: "RoomView",
		components: {},
		data: () => ({}),
		props: {
			element: String,
			resetToggle: Number,
			terminal: Number
		}
	};
</script>

<style lang="scss" scoped>
	.room-container {
		width: 100%;
		padding-top: 95%;
		position: relative;
		background-color: #424242;

		.border {
			position: absolute;
			background-color: #141414;
			&.bottom-left {
				left: 0;
				bottom: 0;
				width: 40%;
				height: 5px;
			}
			&.bottom-right {
				right: 0;
				bottom: 0;
				width: 40%;
				height: 5px;
			}
			&.left {
				top: 0;
				left: 0;
				width: 5px;
				height: 100%;
			}
			&.right {
				top: 0;
				right: 0;
				width: 5px;
				height: 100%;
			}
			&.top {
				top: 0;
				width: 100%;
				height: 5px;
			}
		}

		.terminal {
			width: 12%;
			height: 25%;
			color: #666666;
			position: absolute;
			background-color: #353535;

			&.active {
				color: #dbdbdb;
				box-shadow: 0px 3px 1px -2px rgba(0, 0, 0, 0.2),
					0px 2px 2px 0px rgba(0, 0, 0, 0.14), 0px 1px 5px 0px rgba(0, 0, 0, 0.12);
			}

			.name {
				top: 50%;
				left: 0;
				width: 100%;
				font-size: 24px;
				line-height: 24px;
				position: absolute;
				text-align: center;
				transform: translateY(-50%);
			}

			&:nth-of-type(1) {
				top: 10%;
				right: 5px;
			}

			&:nth-of-type(2) {
				bottom: 10%;
				right: 5px;
			}

			&:nth-of-type(3) {
				top: 33%;
				right: 33%;
				transform: rotate(330deg);

				.name {
					margin-top: -25%;
					transform: rotate(30deg);
				}
			}

			&:nth-of-type(4) {
				top: 53%;
				left: 44%;
				transform: rotate(90deg);

				.name {
					margin-top: -25%;
					transform: rotate(-90deg);
				}
			}

			&:nth-of-type(5) {
				top: 33%;
				left: 33%;
				transform: rotate(30deg);

				.name {
					margin-top: -25%;
					transform: rotate(-30deg);
				}
			}

			&:nth-of-type(6) {
				top: 10%;
				left: 5px;
				.active {
					background-color: #000087;
				}
			}

			&:nth-of-type(7) {
				bottom: 10%;
				left: 5px;
			}
		}
	}

	.theme--arc {
		.terminal {
			&.active {
				background-color: #008f9b;
			}
		}
	}

	.theme--solar {
		.terminal {
			&.active {
				background-color: #a23f00;
			}
		}
	}

	.theme--void {
		.terminal {
			&.active {
				background-color: #4d1a84;
			}
		}
	}
</style>
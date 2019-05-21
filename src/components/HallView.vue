<template>
	<div class="hall-container">
		<div class="room" v-for="(option, i) in rooms" :key="i" :class="{ active: option == room }">
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
		name: "HallView",
		components: {},
		data: () => ({
			rooms: ["green", "white", "yellow", "red", "purple", "blue", "cyan"]
		}),
		props: {
			element: String,
			resetToggle: Number,
			room: String
		},
		watch: {
			element: function() {
				this.reset();
			}
		}
	};
</script>

<style lang="scss" scoped>
	.hall-container {
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

		.room {
			width: 33%;
			height: 24%;
			margin: 1px;
			color: #666666;
			position: absolute;
			box-sizing: border-box;
			background-color: #353535;

			&.active {
				color: #dbdbdb;
				box-shadow: 0px 3px 1px -2px rgba(0, 0, 0, 0.2),
					0px 2px 2px 0px rgba(0, 0, 0, 0.14), 0px 1px 5px 0px rgba(0, 0, 0, 0.12);
			}

			&:nth-child(1) {
				top: 0;
			}

			&:nth-child(2) {
				top: 25.25%;
			}

			&:nth-child(3) {
				top: 50.5%;
			}

			&:nth-child(4) {
				bottom: 0;
			}

			&:nth-child(5) {
				right: 0;
				top: 25.25%;
			}

			&:nth-child(6) {
				right: 0;
				top: 50.5%;
			}

			&:nth-child(7) {
				right: 0;
				bottom: 0;
			}

			.name {
				top: 50%;
				left: 50%;
				font-size: 24px;
				line-height: 24px;
				position: absolute;
				transform: translate(-50%, -50%);
			}
		}
	}

	.theme--arc {
		.room {
			&.active {
				background-color: #008f9b;
			}
		}
	}

	.theme--solar {
		.room {
			&.active {
				background-color: #a23f00;
			}
		}
	}

	.theme--void {
		.room {
			&.active {
				background-color: #4d1a84;
			}
		}
	}
</style>

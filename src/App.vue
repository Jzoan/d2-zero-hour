<template>
	<v-app dark :class="`theme--${element}`">
		<v-toolbar app>
			<v-toolbar-title class="headline text-uppercase">
				<span class="app-name">ZERO HOUR&nbsp;&nbsp;</span>
			</v-toolbar-title>
			<div class="change-element-selector">
				<span
					class="list-item"
					:class="element == 'void' ? 'active' : ''"
					@click="changeElement('void')"
				>Void</span>
				<span class="tiny-pipe">&nbsp;|&nbsp;</span>
				<span
					class="list-item"
					:class="element == 'arc' ? 'active' : ''"
					@click="changeElement('arc')"
				>Arc</span>
				<span class="tiny-pipe">&nbsp;|&nbsp;</span>
				<span
					class="list-item"
					:class="element === 'solar' ? 'active' : ''"
					@click="changeElement('solar')"
				>Solar</span>
				<div class="change-element-slider"></div>
			</div>
			<v-spacer></v-spacer>
		</v-toolbar>

		<v-content>
			<PuzzleSolver :element="element"/>
		</v-content>
	</v-app>
</template>

<script>
	import PuzzleSolver from "./components/PuzzleSolver";

	export default {
		name: "App",
		components: {
			PuzzleSolver
		},
		data: () => ({
			element: "arc"
		}),
		methods: {
			changeElement: function(newElement) {
				this.element = newElement;
			}
		}
	};
</script>

<style lang="scss">
	body {
		-webkit-user-select: none; /* Chrome all / Safari all */
		-moz-user-select: none; /* Firefox all */
		-ms-user-select: none; /* IE 10+ */
		user-select: none; /* Likely future */
	}

	.app-name {
		@media screen and (max-width: 1023px) {
			display: none;
		}
	}

	.change-element-selector {
		width: 100%;
		height: 100%;
		font-size: 22px;
		margin-left: -24px;
		position: absolute;
		text-align: center;

		.list-item {
			height: 100%;
			padding: 0 10px;
			position: relative;
			align-items: center;
			display: inline-flex;
		}

		.tiny-pipe {
			font-size: 11px;
			padding: 0 8px;
		}
	}

	.theme--arc {
		.list-item {
			&.active {
				color: #00c1d1;
				border-top: 2px solid;
			}
		}
	}

	.theme--solar {
		.list-item {
			&.active {
				color: #d15100;
				border-top: 2px solid;
			}
		}
	}

	.theme--void {
		.list-item {
			&.active {
				color: #a800ff;
				border-top: 2px solid;
			}
		}
	}

	.theme--dark.application {
		color: #dbdbdb;
	}

	.theme--light.application {
		color: #595959;
	}
</style>
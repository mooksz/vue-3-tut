<template>
	<div class="app">
		<router-view />
	</div>
</template>

<script>
	export default {
		name: "App",
	};
</script>

<style lang="scss">
	html {
		font-size: 10px;
	}

	body {
		font-size: 1.6rem;
	}

	* {
		box-sizing: border-box;
	}

	.app {
		font-family: Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		color: #2c3e50;
		background-color: lightgray;
	}
</style>

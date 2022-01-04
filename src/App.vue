<template>
	<div id="app">
		<header-nav />
		<stats />
		<div class="chart-container">
			<state />
		</div>
		<footer>
			Powered by <a href="https://covidactnow.org/"> COVID Act Now </a>
		</footer>
	</div>
</template>

<script>
import HeaderNav from './components/header.vue';
import State from './components/state.vue';
import Stats from './components/state-stats.vue';

export default {
	name: 'App',
	components: {
		HeaderNav,
		State,
		Stats,
	}
}
</script>

<style>
	@import url(https://fonts.googleapis.com/css?family=Lato:400,300|Oswald);
	@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200;400;600|Lato:400,300');
	body {
		margin: 0;
		padding: 0;
		border: 0;
		font-size: 100%;
		font: inherit;
		vertical-align: baseline;
		background-color: #f6f6f6;
	}
	#app {
		font-family: 'Montserrat';
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		color: #555;
		padding-bottom: 40px;
	}
	.chart-container {
		margin: 40px auto;
		height: 400px;
		width: 80vw;
		background-color: #fff;
		padding: 20px;
		border-radius: 6px;
		box-shadow: 0px 1px 2px rgba(67, 67, 67, 0.1) ;
	}
	footer {
		text-align: center;
		font-size: 12px;
	}
	a {
		color: #308b9f;
	}
</style>

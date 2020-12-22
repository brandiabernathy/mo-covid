<template>
	<div id="app">
		<header-nav />
		<stats />
		<!-- <county /> -->
		<div class="chart-container">
			<state />
		</div>
	</div>
</template>

<script>
import HeaderNav from './components/header.vue';
import State from './components/state.vue';
// import County from './components/county.vue';
import Stats from './components/stats.vue';

export default {
	name: 'App',
	components: {
		// County,
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
	}
	#app {
		/* font-family: Avenir, Helvetica, Arial, sans-serif; */
		font-family: 'Montserrat';
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		/* text-align: center; */
		color: #555;
		background-color: #f6f6f6;
		/* margin: 60px; */
	}
	.chart-container {
		margin: 40px auto;
		height: 50vh;
		width: 80vw;
		background-color: #fff;
		padding: 20px;
		border-radius: 6px;
		box-shadow: 0px 1px 2px rgba(67, 67, 67, 0.1) ;
	}
</style>

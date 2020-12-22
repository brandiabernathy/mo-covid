
<template>
	<header>
		<div>
			<img src="../assets/missouri.png" />
			<h1>MO COVID</h1>
			<router-link to="/county">Navigate to Page2</router-link>
		</div>
	</header>
</template>
<script>


export default {
	name: 'Header',
	data() {
		return {
		};
	},
}
</script>
<style scoped>
	header {
		height: 70px;
		border-bottom: 1px solid #ddd;
		padding: 0 40px;
		line-height: 70px;
		background-color: #fff;
	}
	h1 {
		display: inline-block;
		vertical-align: middle;
		margin: 0;
	}
	img {
		display: inline-block;
		vertical-align: middle;
		width: 40px;
		margin-right: 10px;
	}
</style>

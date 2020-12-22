<template>
	<div id="app">
		<header>
			<div class="left">
				<router-link to="/">
					<img src="./assets/missouri.png" />
					<h1>MO COVID</h1>
				</router-link>
			</div>
			<nav id="nav">
				<router-link to="/about">About</router-link>
			</nav>
		</header>
		<router-view/>
	</div>
</template>

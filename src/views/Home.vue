<template>
	<div class="home">
		<stats />
		<div class="chart-container">
			<state />
		</div>
	</div>
</template>

<script>
// @ is an alias to /src
import State from '@/components/state.vue';
import Stats from '@/components/state-stats.vue';

export default {
	name: 'Home',
	components: {
		State,
		Stats,
	}
}
</script>

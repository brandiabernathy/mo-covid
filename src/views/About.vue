<template>
	<div class="about">
		<stats />
		<div class="chart-container">
			<county />
		</div>
	</div>
</template>

<script>
// @ is an alias to /src
import County from '@/components/county.vue';
import Stats from '@/components/county-stats.vue';

export default {
	name: 'STLCo',
	components: {
		County,
		Stats,
	}
}
</script>

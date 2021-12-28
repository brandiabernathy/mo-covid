
<template>
	<div class="wrapper">
		<div class="stat"><div class="label">Percent fully vaccinated</div><div class="num">{{ parseFloat(percent_vaccinated).toFixed(1) }}%</div></div>
		<div class="stat"><div class="label">Total cases</div><div class="num">{{ total_cases }}</div></div>
		<div class="stat"><div class="label">Positivity rate (past 7 days)</div><div class="num">{{ parseFloat(positivity_rate).toFixed(1) }}%</div></div>
		<div class="stat"><div class="label">COVID patients hospitalized</div><div class="num">{{ hospitalized }}</div></div>
		<div class="stat"><div class="label">COVID patients in ICU</div><div class="num">{{ icu }}</div></div>
	</div>
</template>
<script>

import axios from 'axios';
import dayjs from 'dayjs';

var customParseFormat = require('dayjs/plugin/customParseFormat')
dayjs.extend(customParseFormat)

export default {
	name: 'Stats',
	data() {
		return {
			total_cases: '',
			percent_vaccinated: '',
			positivity_rate: '',
			positive_tests: [],
			hospitalized: '',
			icu: '',
		};
	},
	created() {
		axios
			.get('https://api.covidactnow.org/v2/state/MO.timeseries.json?apiKey=' + process.env.VUE_APP_API_KEY)
			.then(res => {
				this.icu = res.data.actuals.icuBeds.currentUsageCovid;
				this.hospitalized = this.number_with_commas(res.data.actuals.hospitalBeds.currentUsageCovid);
				this.total_cases = this.number_with_commas(res.data.actuals.cases);
				this.percent_vaccinated = res.data.metrics.vaccinationsCompletedRatio * 100;
				this.icu_beds = res.data.actuals.icuBeds.capacity - res.data.actuals.icuBeds.currentUsageTotal;
				let positivity_rate = res.data.metrics.testPositivityRatio * 100;
				this.positivity_rate = positivity_rate.toFixed(2);
			});
	},
	methods: {
		number_with_commas(x) {
			return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
		}
	}
}
</script>
<style scoped>
	.wrapper {
		width: calc(80vw + 40px);
		margin: 40px auto;
		display: flex;
		justify-content: space-between;
	}
	.stat {
		padding: 20px 20px 12px;
		background-color: #fff;
		border-radius: 6px;
		box-shadow: 0px 1px 2px rgba(67, 67, 67, 0.1) ;
	}
	.stat + .stat {
		margin-left: 15px;
	}
	.num {
		font-size: 50px;
		font-family: 'Lato';
	}
	.label {
		font-weight: 600;
		font-size: 12px;
	}
</style>

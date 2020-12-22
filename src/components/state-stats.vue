
<template>
	<div class="wrapper">
		<div class="stat"><div class="label">Total cases</div><div class="num">{{ total_cases }}</div></div>
		<div class="stat"><div class="label">Positivity rate (past 7 days)</div><div class="num">{{ positivity_rate }}%</div></div>
		<div class="stat"><div class="label">COVID patients hospitalized</div><div class="num">{{ hospitalized }}</div></div>
		<div class="stat"><div class="label">COVID patients in ICU</div><div class="num">{{ icu }}</div></div>
		<div class="stat"><div class="label">ICU beds left</div><div class="num">{{ icu_beds }}</div></div>
		<!-- <div class="stat"><div class="label">Currently on a ventilator</div><div class="num">{{ ventilator }}</div></div> -->
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
			data: '',
			total_cases: '',
			positivity_rate: '',
			positive_tests: [],
			tests_taken: [],
			hospitalized: '',
			icu: '',
			ventilator: '',
			icu_beds: '',
		};
	},
	created() {
		//adec4b65084f4c4dbca7b8cbc350d509
		axios
			.get('https://api.covidactnow.org/v2/state/MO.timeseries.json?apiKey=adec4b65084f4c4dbca7b8cbc350d509')
			.then(res => {
				// console.log('ressss', res);
				this.data = res.data.actualsTimeseries
				// this.ventilator = res.data[0].onVentilatorCurrently;
				this.icu = res.data.actuals.icuBeds.currentUsageCovid;
				this.hospitalized = this.number_with_commas(res.data.actuals.hospitalBeds.currentUsageCovid);
				this.total_cases = this.number_with_commas(res.data.actuals.cases);
				this.icu_beds = res.data.actuals.icuBeds.capacity - res.data.actuals.icuBeds.currentUsageCovid - res.data.metrics.icuHeadroomDetails.currentIcuNonCovid;
				// let length = res.data.actualsTimeseries.length;
				// for(let i = 0; i < 7; i++) {
				// 	this.positive_tests.push(res.data.actualsTimeseries[length - i].newCases)
				// 	this.tests_taken.push(res.data[i].totalTestResultsIncrease);
				// }
				// let sum_positives = this.positive_tests.reduce(function(a, b) {
				// 	return a + b;
				// }, 0);

				// let sum_tests = this.tests_taken.reduce(function(a, b) {
				// 	return a + b;
				// })
				// console.log('sum_positives', sum_positives);
				// console.log('sum_tests', sum_tests);
				let positivity_rate = res.data.metrics.testPositivityRatio * 100;
				this.positivity_rate = positivity_rate.toFixed(2);
				// this.positivity_rate = res.data.metrics.testPositivityRatio * 100;
				// console.log('positive tests', this.positive_tests);
				// console.log('tests taken', this.tests_taken);
				// this.positivity_days = res.data.map(day => day.positiveIncrease);
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

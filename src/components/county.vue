

<script>

import axios from 'axios';
import dayjs from 'dayjs';
import { Bar } from 'vue-chartjs'

var customParseFormat = require('dayjs/plugin/customParseFormat')
dayjs.extend(customParseFormat)


export default {
	name: 'County',
	extends: Bar,
	data() {
		return {
			dayjs: dayjs,
			// state: null,
			dates: null,
			pos_tests: null,
		};
	},
	created() {
		axios
			.get('https://api.covidactnow.org/v2/county/29189.timeseries.json?apiKey=adec4b65084f4c4dbca7b8cbc350d509')
			.then(res => {
				console.log('county res', res.data);
				this.dates = res.data.actualsTimeseries
				.filter(day => day.cases != null)
				.map(day => dayjs(day.date).format('MMM DD'));

				this.pos_tests = res.data.actualsTimeseries
				.filter(day => day.cases != null)
				.map(day => day.newCases);
				
				this.renderChart({
					labels: this.dates,
					datasets: [
						{
							label: 'New cases',
							backgroundColor: '#8ccedc',
							data: this.pos_tests,
						}
					],
				},
				{
				responsive: true,
				maintainAspectRatio: false,
				title: {
					display: true,
					text: 'Daily New Cases',
					fontSize: 14,
					fontFamily: 'Montserrat',
					fontColor: '#555',
				},
				legend: {
					display: false,
				},
				tooltips: {
					backgroundColor: '#fff',
					borderColor: '#ddd',
					borderWidth: 1,
					titleFontFamily: 'Montserrat',
					titleFontColor: '#2c353b',
					bodyFontColor: '#2c353b',
					bodyFontFamily: 'Lato',
					caretPadding: 5,
					displayColors: false,
				},
				scales: {
					yAxes: [{
						gridLines: {
							display: false,
						},
						ticks: {
							display: false,
						}
					}],
					xAxes: [{
						gridLines: {
							display: false,
						},
					}]
				}
				})

				// console.log('this.state_dates', this.state_dates);
				// console.log('this.state_pos_tests', this.state_pos_tests);
		});
	},
}
</script>
<style scoped>
</style>



<script>

import axios from 'axios';
import dayjs from 'dayjs';
import { Bar } from 'vue-chartjs'

var customParseFormat = require('dayjs/plugin/customParseFormat')
dayjs.extend(customParseFormat)


export default {
	name: 'State',
	extends: Bar,
	data() {
		return {
			dayjs: dayjs,
			state: null,
			state_dates: null,
			state_pos_tests: null,
		};
	},
	created() {
		axios
			.get('https://api.covidactnow.org/v2/state/MO.timeseries.json?apiKey=adec4b65084f4c4dbca7b8cbc350d509')
			.then(res => {
				this.state_dates = res.data.actualsTimeseries
				.filter(day => day.cases != null)
				.map(day => dayjs(day.date).format('MMM DD'));

				this.state_pos_tests = res.data.actualsTimeseries
				.filter(day => day.cases != null)
				.map(day => day.newCases);

				this.renderChart({
					labels: this.state_dates,
					datasets: [
						{
							label: 'New cases',
							backgroundColor: '#8ccedc',
							data: this.state_pos_tests,
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
		});
	},
}
</script>

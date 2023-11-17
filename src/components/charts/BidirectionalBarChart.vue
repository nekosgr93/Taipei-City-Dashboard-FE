<script setup>
import { ref, computed } from "vue";
import { useMapStore } from "../../store/mapStore";

const props = defineProps([
	"chart_config",
	"activeChart",
	"series",
	"map_config",
]);

const chartOptions = ref({
	chart: {
		stacked: true,
	},
	colors: ["#008FFB", "#FF4560"],
	plotOptions: {
		bar: {
			horizontal: true,
			barHeight: "80%",
		},
	},
	dataLabels: {
		enabled: false,
	},
	stroke: {
		width: 1,
		colors: ["#fff"],
	},
	grid: {
		xaxis: {
			lines: {
				show: false,
			},
		},
	},
	xaxis: {
		categories: props.chart_config.categories,
	},
	yaxis: {
		min: -5,
		max: 5,
	},
	tooltip: {
		custom: function ({ series, seriesIndex, dataPointIndex, w }) {
			return '<div class="chart-tooltip">' +
				'<h6>' + w.globals.labels[dataPointIndex] + '</h6>' +
				'<span>' + series[seriesIndex][dataPointIndex] + ` ${props.chart_config.unit}` + '</span>' +
				'</div>';
		},
		followCursor: true,
	},
});
</script>

<template>
	<div>
		<apexchart
			type="bar"
			height="270"
			:options="chartOptions"
			:series="series"
		></apexchart>
	</div>
</template>

<style lang="scss" scoped></style>

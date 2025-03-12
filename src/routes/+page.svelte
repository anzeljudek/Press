<script lang="ts">
	import { getElementAtEvent, Line } from 'svelte-chartjs';
	import { Pie } from 'svelte-chartjs';
	import { data } from '$lib/data.js';

	import {
		Chart as ChartJS,
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		PointElement,
		ArcElement,
		CategoryScale
	} from 'chart.js';
	import { each } from 'chart.js/helpers';
	import Layout from './+layout.svelte';

	ChartJS.register(
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		ArcElement,
		PointElement,
		CategoryScale
	);
	type ChartData = {
		labels: (string | number)[];
		datasets: {
			label?: string;
			fill?: boolean;
			borderColor?: string;
			data: number[];
			backgroundColor?: string[];
			hoverBackgroundColor?: string[];
		}[];
	};

	let year: number = 2023;

	let chart1: ChartData = {
		labels: data.map((element) => element.year),
		datasets: [
			{
				label: 'Male',
				fill: false,
				borderColor: 'rgb(54, 162, 235)',
				data: data.map((element) => element.m)
			},
			{
				label: 'Female',
				fill: false,
				borderColor: 'rgb(255, 99, 132)',
				data: data.map((element) => element.f)
			}
			//{
			//label: 'Linija 3',
			//fill: false,
			//borderColor: 'rgb(34, 99, 132)',
			//data: [1, -2, 19, -10, 269]
			//}
		]
	};

	let chart2: ChartData = {
		labels: ['Male', 'Female'],

		datasets: [
			{
				data: [180, 180],
				backgroundColor: ['rgb(52, 161, 235)', 'rgb(235, 83, 52)']
			}
		]
	};
</script>

<div class="container mx-auto">
	<div class="grid grid-cols-2 gap-10 mb-10">
		<div class="border-4 border-violet-200 p-3">
			<h2 class="text-center text-2xl text-violet-700 font-bold">Graf podatkov</h2>
			<Line data={chart1} options={{ responsive: true }} />
		</div>
		<div class="border-4 border-violet-200 p-3">
			<h2 class="text-center text-2xl text-violet-700 font-bold">Graf podatkov</h2>
			<input class="w-full text-center border-white-700" type="number" bind:value={year} />
			<Pie data={chart2} options={{ responsive: true }} />
		</div>
	</div>
</div>

{#each data as year}
	<p>{year.year} rojenih: {year.f} deklet in {year.m} fantov</p>
{/each}

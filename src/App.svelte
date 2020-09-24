<script>
	import Header from './header.svelte';
	import BarChart from './barChart.svelte';
	import PieChart from './pieChart.svelte';
	import axios from 'axios';
	import { onMount } from 'svelte';

	let show = false;
	let covidData = [];
	// $: visit = count;
	$: covidData;

	const handleClick = () => {
		show = !show;
	};

	onMount(async () => {
		await axios.get(`https://api.covid19api.com/total/country/india`)
		.then(res => covidData = res.data)
		.catch(error=>console.error(error));
	});

</script>

<main>
	<Header />
	<button disabled ={show} class="btn" on:click={handleClick}>India Covid Info</button>
	{#if show}
	<div class="chart-container">
		<div class="items">
			<BarChart covidData={(covidData)} />
		</div>	
		<div class="items">
			<PieChart covidData={(covidData)} />
		</div>
	</div>
	{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
		background-color: #E0E0E0;
		height: auto;
		font-family: cursive;

	}

	.chart-container {
		margin-top: 30px;
    	display: flex;
    	padding: 10px;
	}

	.items {
		display: flex;
    	flex-wrap: nowrap;
		flex-direction: column;
		flex-grow: 1;
		border: 1px solid #ffb300;
    	box-shadow: 0px 0px 0px 2px #ffb300;
	}

	.btn {
		border-radius: 8px;
    	background-color: darkgrey;
    	color: white;
    	font-family: cursive;
		font-weight: 700;
		cursor: pointer;
	}

	.img {
        height: 400px;
        width: 100%;
    }

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
	@media (max-width: 920px) {
		.chart-container {
			flex-direction: column;
		}
	}
</style>
<script>
  import Header from "./header.svelte";
  import BarChart from "./barChart.svelte";
  import PieChart from "./pieChart.svelte";
  import axios from "axios";
  import { onMount, beforeUpdate } from "svelte";

  let show = false;
  let covidData = [];
  let totalData = [];
  // $: visit = count;
  $: covidData;
  $: totalData;

  const handleClick = () => {
    show = !show;
  };

  onMount(async () => {
    await axios
      .get(`https://api.covid19api.com/total/country/india`)
      .then(res => (covidData = res.data))
      .catch(error => console.error(error));
  });

  beforeUpdate(async () => {
    await axios
      .get(`https://api.covidindiatracker.com/total.json`)
      .then(res => (totalData = res.data))
      .catch(error => console.error(error));
  });
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
    background-color: #e0e0e0;
    height: auto;
    font-family: cursive;
  }

  @media only screen and (max-width:600px) {
	  main {
    text-align: center;
    padding: 1em;
    max-width: 700px;
    margin: 0 auto;
    background-color: #e0e0e0;
    height: auto;
    font-family: cursive;
  }
  .chart-container {
    margin-top: 30px;
    display: flex;
    padding: 5px;
	margin-bottom: 10px;
  }
  }

  .chart-container {
    margin-top: 30px;
    display: flex;
    padding: 10px;
  }

  .info-container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
	flex-wrap: wrap;
  }

  .info-container .info-item {
    display: flex;
    flex-direction: column;
    flex: 1 1 200px;
    margin: 1em;
    box-shadow: 0 0px 10px 1px rgba(0, 0, 0, 0.2);
    align-items: center;
    border-radius: 8px;
    color: #0171ba;
    text-align: center;
    padding: 20px;
    transition: 1s ease;
  }

  .red {
    color: red !important;
	 background: linear-gradient(to bottom, #ff8582 0%, #fe8685 16%, #ff908e 44%, #fe908f 53%, #ff9692 62%, #ff9597 67%, #ff9a98 84%, #ff9b9b 85%, #fe9c9d 91%, #ff9e98 96%, #ff9d9c 96%, #ff9e9d 100%);
  }

  .green {
    color: green !important;
	background : linear-gradient(to bottom, #9ae69c 0%, #9ce999 5%, #9cea9e 6%, #9cea9e 6%, #a0e99a 10%, #a3eb95 24%, #adee92 36%, #adee90 40%, #b3ef8f 45%, #b0f08f 46%, #b4f18a 50%, #b7f18d 51%, #b6f08a 53%, #baf18b 58%, #c4f780 77%, #c9f681 86%, #ccfa7e 90%, #cbf77c 94%, #cff87e 96%, #cff87e 100%)
  }

  .orange {
	color: saddlebrown !important;
	background-color: #FFB973;
    background: linear-gradient(to bottom, rgba(255,175,75,1) 0%, rgba(255,146,10,1) 100%);
  }

  .blue {
	    background: linear-gradient(to bottom, #a5c9fd 0%, #a5c9fd 6%, #a7cbff 8%, #a5c9fd 11%, #a7cbff 11%, #aacffc 28%, #b0d5ff 44%, #b0d6fb 48%, #b5dbff 62%, #b4dbfc 62%, #b8dffe 75%, #bae2fb 79%, #bce4fe 91%, #bde6fa 96%, #bee7fd 100%);
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

<main>
  <Header />
  <button disabled={show} class="btn" on:click={handleClick}>
    India Covid Info
  </button>
  {#if show}
    <div class="info-container">
      <div class="info-item blue">
        <strong>Total Cases</strong>
        <strong>{totalData.confirmed}</strong>
      </div>
      <div class="info-item orange">
        <strong>Active</strong>
        <strong>{totalData.active}</strong>
      </div>
      <div class="info-item green">
        <strong>Recoveries</strong>
        <strong>{totalData.recovered}</strong>
      </div>
      <div class="info-item red">
        <strong>Deaths</strong>
        <strong>{totalData.deaths}</strong>
      </div>
    </div>
    <div class="chart-container">
      <div class="items">
        <BarChart {covidData} />
      </div>
      <div class="items">
        <PieChart {covidData} />
      </div>
    </div>
  {/if}
</main>

<canvas id="lineChart" width="500" height="300"></canvas>

<script>
    import Chart from 'chart.js';
    import { afterUpdate } from 'svelte';
    export let covidData;

    var ctx;
    var lineChart;
    function createChart() {
    ctx = document.getElementById('lineChart');
    let labels = covidData.map(t => t.Date);
    let cases = covidData.map(t => t.Confirmed);
    let active = covidData.map(t => t.Active);
    let Recovered = covidData.map(t => t.Recovered);
    let Deaths = covidData.map(t => t.Deaths);
    
    lineChart = new Chart(ctx, {
    type: 'line',
    data: {
        labels: labels,
        datasets: [{
            label: 'Confirmed Cases',
            backgroundColor: 'rgb(255, 99, 132)',
            borderColor: 'rgb(255, 99, 132)',
            color: 'rgb(255,255,255)',
            borderDash: [1, 1],
            fill: false,
            data: cases, 
        },
        {
            label: 'Active Cases',
            backgroundColor: 'rgb(255,178,102)',
            borderColor: 'rgb(255,178,102)',
            color: 'rgb(255,255,255)',
            borderDash: [1, 1],
            fill: false,
            data: active, 
        },
        {
            label: 'Recovered Cases',
            backgroundColor: 'rgb(0,255,0)',
            borderColor: 'rgb(0,255,0)',
            color: 'rgb(255,255,255)',
            borderDash: [1, 1],
            fill: false,
            data: Recovered, 
        },
        {
            label: 'Deaths Cases',
            backgroundColor: 'rgb(0,0,204)',
            borderColor: 'rgb(0,0,204)',
            color: 'rgb(255,255,255)',
            borderDash: [1, 1],
            fill: false,
            data: Deaths, 
        }
    ]
    },
    options: {
      responsive: true, 
      maintainAspectRatio: true,
      scales: {
        xAxes: [{
          scaleLabel: {
            display: true,
            labelString: 'Date'
          }
        }],
        yAxes: [{
          scaleLabel: {
            display: true,
            labelString: 'No. of cases'
          }
        }]
      },
    }
});
}
afterUpdate(createChart);
</script>
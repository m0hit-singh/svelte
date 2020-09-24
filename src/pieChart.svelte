<canvas id="pieChart" width="500" height="300"></canvas>

<script>
    import Chart from 'chart.js';
    import { afterUpdate } from 'svelte';
    export let covidData;
    let data = covidData;
    var ctx;
    var pieChart;
    function createPiChart() {
    ctx = document.getElementById('pieChart');
    let totalCases = data.sort((a,b) => b.Confirmed - a.Confirmed)[0];

    pieChart = new Chart(ctx, {
    type: 'doughnut',
    data: {
        labels: ['Confirmed', 'Active', 'Deaths', 'Recovered'],
        datasets: [{
      backgroundColor: [
        "#95a5a6",
        "#3498db",
        "#e74c3c",
        "#2ecc71",
      ],
      data: [totalCases.Confirmed, totalCases.Active, totalCases.Deaths, totalCases.Recovered]
    }]
    },   
    options: {}
});
}
afterUpdate(createPiChart);
</script>
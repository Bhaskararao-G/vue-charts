<template>
  <div class="hello">
    <LineChart
      v-if="loaded"
      :chartdata="chartdata"
      :options="options"
    />
  </div>
</template>

<script>

import LineChart from './LineChart.vue'

export default {
  name: 'HelloWorld',
  data: () => ({
    loaded: false,
    chartdata: null,
    options: {
      responsive: true,
      maintainAspectRatio: false,
      legend: {
        position: "bottom",
        labels: {
          boxWidth: 8,
          fontColor: "red",
          fontStyle: "bold",
          generateLabels: function(chart){
            var data = chart.data;
            var legends = Array.isArray(data.datasets) ? data.datasets.map(function(dataset, i) {
              return {
                text: dataset.label,
                fillStyle: "gray",
                lineWidth: 3,
                strokeStyle: dataset.color,
                hidden: !chart.isDatasetVisible(i),
              };
            }, this) : [];
            return legends;
          },
          usePointStyle: true
        }
      }
    }
  }),
  mounted () {
    this.loaded = true;
    this.chartdata = {
      labels: ['January', 'February', 'March', 'April', 'May'],
      datasets: [
        {
          label: 'One',
          data: [40, 20, 10, 20, 50],
          color: 'blue'
        },
        {
          label: 'Two',
          data: [10, 30, 15, 25, 60],
          color: 'green'
        },
        {
          label: 'Three',
          data: [25, 35, 55, 15, 75],
          color: 'skyblue'
        },
        {
          label: 'Four',
          data: [45, 5, 45, 65, 55],
          color: 'brown'
        }
      ]
    }
  },
  components: {
    LineChart
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

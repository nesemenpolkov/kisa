<template>
  <!-- svoi kod dizaina -->
  <div v-if="!loading" class="plotBox">
    <Line
        :chart-data="chartData"
        :width="30"
        :height="30"
    />
  </div>
  <div v-else>
    Click to build plot...
  </div>
  <button @click="buildChart">Click me</button>
</template>

<script>
import axios from "axios";
import { Line } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  PointElement,
  CategoryScale
} from 'chart.js'

ChartJS.register(
    Title,
    Tooltip,
    Legend,
    LineElement,
    LinearScale,
    PointElement,
    CategoryScale
)
export default {
  name: 'App',
  components: { Line },
  data() {
    return {
      loading: true,
      chartData: {
        labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979',
            data: [40, 39, 10, 40, 39, 80, 40]
          }
        ]
      }
    }
  },
  methods: {
    buildChart() {
      try {
        this.loading = true;
        const response = axios.get("your url address", {
          params: {
            some_param: "param"
          }
        });
        if (response.status === 200) {
          let temp = {...this.chartData};
          temp.labels = [...this.response.labels];
          temp.datasets[0].label = "some string or variable for Kisa data";
          temp.datasets[0].data = [...response.data];
          this.chartData = { ...temp };
        }
      } finally {
        this.loading = false;
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.plotBox {
  height: 500px;
  width: 500px;
  border-style: double;
  border: 3px teal;
  box-shadow: 7px 10px lightgrey;

}
</style>

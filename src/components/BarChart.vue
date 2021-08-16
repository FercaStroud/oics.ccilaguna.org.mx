<script>
import { Bar } from 'vue-chartjs'
export default {
  extends: Bar,
  props:{
    labels: [],
    rates: [],
  },
  data() {
    return {
      chartData: {
        labels: this.labels,
        datasets: [{
          label: 'Calificación',
          borderWidth: 1,
          backgroundColor: [
            'rgba(0, 174, 210, 0.2)',
            'rgba(255, 52, 176, 0.2)',
            'rgba(0, 71, 134, 0.2)',
          ],
          borderColor: [
            'rgba(0, 174, 210,1)',
            'rgba(255, 52, 176, 1)',
            'rgba(0, 71, 134, 1)',
          ],
          pointBorderColor: '#2554FF',
          data: this.rates
        }]
      },
      options: {
        tooltips: {
          callbacks: {
            label: function(tooltipItem, data) {
              return "Ver más detalles en Documentos";
            }
          }
        },
        scales: {
          yAxes: [{
            ticks: {
              beginAtZero: true,
              max: 10
            },
            gridLines: {
              display: true
            }
          }],
          xAxes: [{
            gridLines: {
              display: false
            }
          }]
        },
        legend: {
          display: false
        },
        responsive: true,
        maintainAspectRatio: false
      }
    }
  },
  mounted() {
    this.renderChart(this.chartData, this.options)
  }
}
</script>

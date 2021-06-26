<script>
import {Doughnut} from 'vue-chartjs'

export default {
  extends: Doughnut,
  mounted() {
    this.renderChart(
        {
          labels: ['Transparencia y Acceso a la Información', 'Participación Ciudadana', 'Rendición de Cuentas', 'Rendimiento'],
          datasets: [
            {
              backgroundColor: [
                '#41B883',
                '#E46651',
                '#00D8FF',
                '#DD1B16'
              ],
              data: [25, 25, 25, 25]
            }
          ]
        },
        {
          title: {
            display: false,
          },
          tooltips: {
            callbacks: {
              label: function(tooltipItem, data) {
                return data.labels[tooltipItem.index];
              }
            }
          },
          onClick: (e, data) => {
            this.$emit('updateTextInDoughnut', data)
          },
          responsive: true,
          maintainAspectRatio: false
        }
    )
  }
}
</script>

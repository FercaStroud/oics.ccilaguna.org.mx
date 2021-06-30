<template lang="pug">
  section#quienes.p-5
    .container
      b-row(align-v="center")
        b-col(md="8")
          .text-left(style="margin-bottom:10px")
            strong.title Proyecto
          .text-left.text-container
            p(style="text-align:justify") El Tablero de Evaluación y Seguimiento de los Órganos Internos de Control Municipal del Estado de Coahuila es un modelo dinámico que evalúa el desempeño de los OICs en el ámbito municipal, en la primera etapa contempla los municipios de Saltillo , Torreón , Matamoros a través del monitoreo de 95 indicadores agrupados en 4 ejes temáticos.

        b-col(md="4")
          b-img(
            style="width:100%"
            rounded
            src="@/assets/images/quienessomos.jpg"
            alt="Responsive image"
          )
      b-row(align-v="center")
        b-col(md="12" style="text-align:left")
          strong.title Ejes evaluados:
        b-col(md="6")
          doughnut-chart(
            v-on:updateTextInDoughnut="updateTextInDoughnut"
          )
        b-col(md="6")
          p(style="text-align:left !important;")
            strong {{ textInDoughnut.title }}
          p(style="text-align:justify !important;") {{ textInDoughnut.description }}
      b-row(align-v="center")
        b-col(md="12")
          .text-left.text-container
            br/
            p(style="text-align:justify !important;") La independencia de la entidad resulta una precondición para alcanzar sus objetivos y misión,pues de ello se deriva el nivel de autonomía del que dispondrá para administrar su labor y desarrollar sus funciones.
</template>

<script>
import DoughnutChart from "../components/DoughnutChart";

export default {
  components: {DoughnutChart},
  name: "AboutUs",
  data: function () {
    return {
      textInDoughnut:{title:'',description:''} ,
    }
  },
  methods: {
    updateTextInDoughnut: function (data) {
      switch (data[0]._index) {
        case 0:
          this.textInDoughnut = {
            title: 'TRANSPARENCIA Y ACCESO A LA INFORMACIÓN',
            description: 'Construir un buen gobierno implica la apertura de su actuación al escrutinio público a través de mecanismos que garanticen a los ciudadanos accesibilidad total al ejercicio de la función pública e impulsen esquemas de corresponsabilidad en la elaboración de políticas públicas encaminadas a la formación de una conducta ética en el funcionamiento administrativo, transparencia en la asignación y el manejo de recursos públicos, así como la rendición de cuentas de acuerdo a las metas establecidas en el corto,mediano y largo plazos.\n' +
                '\n' +
                'La TRANSPARENCIA hace referencia a la disponibilidad de información a través de la cual el OIC hace visibles y accesibles -de manera suficiente, oportuna, clara y adecuada susacciones,políticas, procedimientos y decisiones.',
          }
          break;
        case 1:
          this.textInDoughnut = {
            title: 'PARTICIPACIÓN CIUDADANA',
            description: 'Se refiere a la dimensión de apertura del OIC para incorporarmecanismos e instancias de cooperación y de articulación que faciliten elejercicio de un controlactivo por parte de los ciudadanos y organizaciones de la sociedad civil. Es imprescindiblegarantizar la participación activa de la ciudadanía a fin de perfeccionar la calidad del control, y su involucramiento coadyuva a una mayor cultura de transparencia gubernamental.',
          }
          break;
        case 2:
          this.textInDoughnut = {
            title: 'RENDICIÓN DE CUENTAS',
            description: 'Se refiere a los ejercicios mediante los cuales el OIC se responsabiliza de su accionar frente a la ciudadanía -principal beneficiaria de la tarea de control,a través de dispositivos institucionales que permiten dar a conocer intensamente losprocedimientosy actividades que desempeña.En particular, la rendición de cuentas comprende la existencia de prácticas y mecanismos através de los cuales la entidades activamente transparente respecto de su funcionamiento interno,iniciando procedimientos de comunicación con el público y difundiendo ampliamente sus procesos y resultados.',
          }
          break;
        case 3:
          this.textInDoughnut = {
            title: 'RENDIMIENTO',
            description: 'Se refiere al desempeño del OIC respecto de las facultades y funciones quele competen, así como la operatividad en los procedimientos que lleva a cabo. El rendimiento comprendeel funcionamiento mismo de la institución. Contempla la existencia de prácticas y mecanismos de gestión, y examina los procedimientos que permiten garantizar una labor de control imparcial y efectiva que maximice un desempeño integral sólido.',
          }
          break;

      }
    },
  }
}
</script>

<style scoped>

</style>

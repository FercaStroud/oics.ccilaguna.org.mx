<template lang="pug">
  section#tabla-comparativa.p-5(style="background: ghostwhite")
    .container
      b-row(align-v="center")
        b-col(md="12")
          .text-left(style="margin-bottom:10px")
            strong.title Tablero de evaluación y seguimiento de los Órganos Internos de Control Municipal de Coahuila
        b-col(md="12")
          .text-left.text-container Comparativo semestral de la información

      b-row.mt-3(align-v="center")
        b-col
          b-table(:items='items' :fields='fields' responsive bordered)
            template(#thead-top='data')
              b-tr
                b-th(colspan="1")
                b-th(colspan="3" style="background-color:rgba(0, 174, 210,1); color:white") Torreón
                b-th(colspan="3" style="background-color:rgba(255, 52, 176, 1); color:white") Matamoros
                b-th(colspan="3" style="background-color:rgba(0, 71, 134, 1); color:white") Saltillo

            template(#cell(saltillo_junio_2021)='data')
              b-avatar(
                v-if="data.value >= 8.1"
                variant="success"
                :text="data.value"
              )
              b-avatar(
                v-else-if="data.value >= 6.1"
                variant="warning"
                :text="data.value"
              )
              b-avatar(
                v-else
                variant="danger"
                :text="data.value"
              )

            template(#cell(torreon_junio_2021)='data')
              b-avatar(
                v-if="data.value >= 8.1"
                variant="success"
                :text="data.value"
              )
              b-avatar(
                v-else-if="data.value >= 6.1"
                variant="warning"
                :text="data.value"
              )
              b-avatar(
                v-else
                variant="danger"
                :text="data.value"
              )

            template(#cell(matamoros_junio_2021)='data')
              b-avatar(
                v-if="data.value >= 8.1"
                variant="success"
                :text="data.value"
              )
              b-avatar(
                v-else-if="data.value >= 6.1"
                variant="warning"
                :text="data.value"
              )
              b-avatar(
                v-else
                variant="danger"
                :text="data.value"
              )
            template(#cell(saltillo_diciembre_2022)='data')
              b-avatar(
                v-if="data.value >= 8.1"
                variant="success"
                :text="data.value"
              )
              b-avatar(
                v-else-if="data.value >= 6.1"
                variant="warning"
                :text="data.value"
              )
              b-avatar(
                v-else
                variant="danger"
                :text="data.value"
              )

    .container
      b-row(align-v="center")
        b-col(md="12")
        .text-left.text-container(style="font-weight:bolder") Puntaje
      b-row(align-v="center")
        b-col.text-left(md="2" sm="2" style)
          span 8.1 a 10
          b-avatar(
            style="margin-left:10px"
            variant="success"
            text=" "
          )
        b-col.text-left(md="2" sm="2" style)
          span 6.1 a 8
          b-avatar(
            style="margin-left:10px"
            variant="warning"
            text=" "
          )
        b-col.text-left(md="2" sm="2" style)
          span 0 a 6
          b-avatar(
            style="margin-left:10px"
            variant="danger"
            text=" "
          )



</template>

<script>
export default {
  name: "ComparisonTable",
  data: function () {
    return {
      items: [
        {
          eje: 'Transparencia',

          torreon_junio_2021: 7.6,
          torreon_diciembre_2021: null,
          torreon_junio_2022: null,

          matamoros_junio_2021: 6.0,
          matamoros_diciembre_2021: null,
          matamoros_junio_2022: null,

          saltillo_junio_2021: 7.9,
          saltillo_diciembre_2021: null,
          saltillo_junio_2022: null,
        },
        {
          eje: 'Participación Ciudadana',
          saltillo_junio_2021: 8.7,
          saltillo_diciembre_2021: null,
          saltillo_junio_2022: null,

          torreon_junio_2021: 8.7,
          torreon_diciembre_2021: null,
          torreon_junio_2022: null,

          matamoros_junio_2021: 7.9,
          matamoros_diciembre_2021: null,
          matamoros_junio_2022: null,

        },
        {
          eje: 'Rendición de Cuentas',
          saltillo_junio_2021: 7.9,
          saltillo_diciembre_2021: null,
          saltillo_junio_2022: null,

          torreon_junio_2021: 8.2,
          torreon_diciembre_2021: null,
          torreon_junio_2022: null,

          matamoros_junio_2021: 6.6,
          matamoros_diciembre_2021: null,
          matamoros_junio_2022: null,

        },
        {
          eje: 'Rendimiento',
          saltillo_junio_2021: 8.8,
          saltillo_diciembre_2021: null,
          saltillo_junio_2022: null,

          torreon_junio_2021: 8.6,
          torreon_diciembre_2021: null,
          torreon_junio_2022: null,

          matamoros_junio_2021: 7.3,
          matamoros_diciembre_2021: null,
          matamoros_junio_2022: null,

        },
      ],
      fields: [
        { key: 'eje', label: 'Eje' },

        { key: 'torreon_junio_2021', label: 'Junio 2021' },
        { key: 'torreon_diciembre_2021', label: 'Diciembre 2021' },
        { key: 'torreon_junio_2022', label: 'Junio 2022' },

        { key: 'matamoros_junio_2021', label: 'Junio 2021' },
        { key: 'matamoros_diciembre_2021', label: 'Diciembre 2021' },
        { key: 'matamoros_junio_2022', label: 'Junio 2022' },

        { key: 'saltillo_junio_2021', label: 'Junio 2021' },
        { key: 'saltillo_diciembre_2021', label: 'Diciembre 2021' },
        { key: 'saltillo_junio_2022', label: 'Junio 2022' },
      ]
    }
  },
  methods: {
  }
}
</script>

<style scoped>

</style>

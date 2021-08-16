<template lang="pug">
  section#documentos.p-5(style="background: ghostwhite")
    .container
      b-row(align-v="center")
        b-col(md="12")
          .text-left(style="margin-bottom:10px")
            strong.title Documentos
          .text-left.text-container
            //p Sin datos por el momento.
        b-col(md="12")
          b-table(hover responsive striped :items="documents.items" style="background:white;")
            template(v-slot:head(title)="data")
              strong Título
            template(v-slot:head(text)="data")
              strong Descripción
            template(v-slot:head(href)="data")
              strong Acciones

            template(v-slot:cell(title)="data")
              strong {{ data.item.title }}

            template(v-slot:cell(href)="data")
              b-button(
                block
                :href="data.value"
                target="_blank"
                variant="primary"
                style="color:white !important;"
              ) Ver
</template>

<script>
export default {
  name: "Documents",
  data: function () {
    return {
      documents: {
        items: [
          {
            title: 'Documento 1 - PDF',
            text: 'Diagnóstico y recomendaciones SOBRE EL FUNCIONAMIENTO DE LA Contraloría Municipal DE MATAMOROS, COAHUILA',
            href: 'https://oics.ccilaguna.org.mx/MATAMOROS.pdf'
          },
          {
            title: 'Documento 2 - PDF',
            text: 'Diagnóstico y recomendaciones SOBRE EL FUNCIONAMIENTO DE LA Contraloría Municipal DE SALTILLO, COAHUILA',
            href: 'https://oics.ccilaguna.org.mx/SALTILLO.pdf'
          },
          {
            title: 'Documento 3 - PDF',
            text: 'Diagnóstico y recomendaciones SOBRE EL FUNCIONAMIENTO DE LA Contraloría Municipal DE TORREÓN, COAHUILA',
            href: 'https://oics.ccilaguna.org.mx/TORREON.pdf'
          },
          {
            title: 'Documento 4 - EXCEL',
            text: 'Justificación de Calificaciones',
            href: 'https://oics.ccilaguna.org.mx/Justificación de Calificaciones.xlsx'
          },
        ]
      }
    }
  }
}
</script>

<style scoped>

</style>

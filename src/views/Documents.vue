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
            title: 'Documento 1',
            text: 'Diagnóstico y recomendaciones sobre el funcionamiento de la Contraloría Municipal de Matamoros',
            href: 'https://oics.ccilaguna.org.mx/documento_uno.pdf'
          },
          {
            title: 'Documento 2',
            text: 'Diagnóstico y recomendaciones sobre el funcionamiento de la Contraloría Municipal de Saltillo',
            href: 'https://oics.ccilaguna.org.mx/documento_dos.pdf'
          },
        ]
      }
    }
  }
}
</script>

<style scoped>

</style>

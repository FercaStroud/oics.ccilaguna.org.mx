<template lang="pug">
  header
    b-navbar(toggleable='lg' type='light' fixed="top" style="background:white;")
      .container-fluid()
        b-navbar-brand.navbar-brand-title(href='#' tag="h1" style=" line-height: 36px !important;" )  Tablero de Evaluación y Seguimiento
          .small(style="font-size:.5em;margin-top:-10px; text-align:left") de los Órganos Internos de Control Municipal del Estado de Coahuila
        b-navbar-toggle(target='nav-collapse')
        b-collapse#nav-collapse(is-nav='')
          // Right aligned nav items
          b-navbar-nav.ml-auto
            b-nav-item.hvr-underline-from-left(href='#quienes') Proyecto
            b-nav-item.hvr-underline-from-left(href='#mediciones') Indicadores
            b-nav-item.hvr-underline-from-left(href='#documentos') Documentos
            b-nav-item.hvr-underline-from-left(href='#contacto') Contacto

</template>

<script>
export default {
name: "Navigator"
}
</script>

<style scoped>

</style>

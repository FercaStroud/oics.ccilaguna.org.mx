<template lang="pug">
  header
    b-navbar(toggleable='lg' type='light' fixed="top" style="background:white")
      .container
        b-navbar-brand.navbar-brand-title(href='#' tag="h1" class="mb-0") OICs
        b-navbar-toggle(target='nav-collapse')
        b-collapse#nav-collapse(is-nav='')
          // Right aligned nav items
          b-navbar-nav.ml-auto
            b-nav-item.hvr-underline-from-left(href='#quienes') ¿Quiénes somos?
            b-nav-item.hvr-underline-from-left(href='#mediciones') Mediciones
            b-nav-item.hvr-underline-from-left(href='#contacto') Contacto
            b-nav-item.hvr-underline-from-left(href='#documentos') Documentos

</template>

<script>
export default {
name: "Navigator"
}
</script>

<style scoped>

</style>
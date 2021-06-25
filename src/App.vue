<template lang="pug">
  #app
    Navigator
    router-view
    FloatingSocialIcons
    section#privacy.p-3(style="background-color: #f7f7f7;")
      .container
        a(href="#") Aviso de Privacidad
</template>

<style lang="scss">

</style>
<script>
import Navigator from "@/components/Navigator";
import FloatingSocialIcons from "@/components/FloatingSocialIcons";

export default {
  components: {FloatingSocialIcons, Navigator}
}
</script>

<template lang="pug">
  #app
    Navigator
    router-view
    FloatingSocialIcons
    div(style="height:100px")
    footer(style="position:fixed; bottom:0px;background-color:#f7f7f8; width:100%;")
      b-container
        b-row
          b-col(md="2" v-if="note")
            b-img(
              fluid
              center
              src="@/assets/images/logo.png"
              alt="OICS"
              style="margin-top:18px"
            )
          b-col(md="10" v-if="note")
            p
            p La elaboración de este producto ha sido posible gracias al generoso Pueblo de los Estados Unidos de América a través de la Agencia de los Estados Unidos para el Desarrollo Internacional (USAID). El contenido del mismo es responsabilidad del Consejo Cívico de las Instituciones, A.C., y no necesariamente refleja el punto de vista de USAID o del Gobierno de los Estados Unidos.
          b-col(md="10" v-if="!note")
            p
            p Nota aclaratoria: La información cargada en el Tablero de los Órganos Internos de Control municipales está actualizada al mes de junio del año 2021 por lo que es posible que la información pueda ser actualizada o modificada por parte de las instituciones.
          b-col(md="2" v-if="!note")
            b-button(@click="note = !note" style="margin-top:18px") Aceptar
</template>

<style lang="scss">
@media (max-width: 991px) {
  footer{
    display: none;
  }
}
</style>
<script>
import CookieLaw from 'vue-cookie-law'
import Navigator from "@/components/Navigator";
import FloatingSocialIcons from "@/components/FloatingSocialIcons";

export default {
  components: {FloatingSocialIcons, Navigator, CookieLaw},
  data: function () {
    return {
      note: false
    }
  }
}
</script>

<template lang="pug">
  #app
    Navigator
    router-view
    FloatingSocialIcons
    div(style="height:120px")
      a(@click="showDisclaimer" style="cursor:pointer") Ver Disclaimer
    div(v-if="note" style="position:fixed; bottom:0px;background-color:#ECECEC; width:100%;")
      b-container
        b-row
          b-col(md="2" )
            b-img(
              fluid
              center
              src="@/assets/images/logo.png"
              alt="OICS"
              style="margin-top:28px"
            )
          b-col(md="8")
            p
            p(style="text-align:justify") La elaboración de este producto ha sido posible gracias al generoso Pueblo de los Estados Unidos de América a través de la Agencia de los Estados Unidos para el Desarrollo Internacional (USAID). El contenido del mismo es responsabilidad del Consejo Cívico de las Instituciones, A.C., y no necesariamente refleja el punto de vista de USAID o del Gobierno de los Estados Unidos.
          b-col(md="2" )
            b-button(@click="note=false" style="margin-top:35px") Ocultar

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
  },
  methods:{
    showDisclaimer: function(){
      this.note = true;
      console.log("hola")
    }
  }
}
</script>

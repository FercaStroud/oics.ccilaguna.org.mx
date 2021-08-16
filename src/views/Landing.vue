<template lang="pug">
  div
    //slider
    b-carousel#inicio(
      style='text-shadow: 0px 0px 2px #000;margin-top:100px'
      indicators=''
    )
      b-carousel-slide(text='' img-src='@/assets/images/banner.jpg')

    AboutUs
    ComparisonTable
    Measurements
    Documents
    Contact

    //patreons
    section#patrocinadores.p-5(style="")
      .container
        b-row(align-v="center" )
          b-col(md="6")
            .text-left(style="margin-bottom:10px")
              //strong.title Patrocinador
            .text-left.text-container
              //p Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor.
        b-row(align-v="center" )
          b-col(md="4" sm="6")
            b-img(
              fluid
              center
              src="@/assets/images/logo.png"
              alt="OICS"
            )
          b-col(md="4" offset-md="4" sm="6")
            b-img(
              fluid
              center
              src="@/assets/images/consejo.png"
              alt="Consejo Cívico"
            )
    section#privacy.p-3(style="")
      .container
        a(href="/aviso-de-privacidad") Aviso de Privacidad

</template>

<script>
import Measurements from "@/views/Measurements";
import AboutUs from "@/views/AboutUs";
import Documents from "@/views/Documents";
import Contact from "@/views/Contact";
import ComparisonTable from "@/views/ComparisonTable";

export default {
  name: 'Landing',
  components: {ComparisonTable, Contact, Documents, AboutUs, Measurements},
}
</script>

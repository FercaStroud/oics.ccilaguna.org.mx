<template lang="pug">
  div
    //slider
    b-carousel#inicio(
      style='text-shadow: 0px 0px 2px #000'
      indicators=''
      img-width='1024'
      img-height='480'
    )
      b-carousel-slide(text='Catedral de Santiago Apósto. Saltillo, Coahuila' img-src='@/assets/images/banner.jpg')
      b-carousel-slide(text='Catedral de Santiago Apósto. Saltillo, Coahuila' img-src='@/assets/images/banner.jpg')


    //AboutUs
    section#quienes.p-5
      .container
        b-row(align-v="center")
          b-col(md="6")
            .text-left(style="margin-bottom:10px")
              strong.title ¿Quiénes somos?
            .text-left.text-container
              p Buscamos mejorar y optimizar la información generada por los órganos internos de control municipal, así como dar a conocer dicha información de una manera organizada a la ciudadanía en general.
          b-col(md="6")
            b-img(
              style="width:100%"
              rounded
              src="@/assets/images/quienessomos.jpg"
              alt="Responsive image"
            )

    section#mediciones.p-5(style="background: ghostwhite")
      .container-fluid
        b-row(align-v="center")
          b-col(md="12")
            .text-left(style="margin-bottom:10px")
              strong.title Mediciones en Coahuila
            .text-left.text-container
              //p Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula.
        b-row(align-v="center")
          b-col
            b-tabs(content-class='mt-3' fill='')
              b-tab(title='Transparencia' active='')
                b-table(responsive striped :items="measurements.transparency.items")
                  template(#head(entry)="data")
                    span.brand-color Rubro
                  template(#head(question)="data")
                    span.brand-color Pregunta
                  template(#head(information_torreon)="data")
                    span.brand-color Información Municipio (Torreón)
                  template(#head(information_matamoros)="data")
                    span.brand-color Información Municipio (Matamoros)
                  template(#head(information_saltillo)="data")
                    span.brand-color Información Municipio (Saltillo)
                  template(#head(rate_torreon)="data")
                    span.brand-color Codificación Municipio (Torreón)
                  template(#head(rate_matamoros)="data")
                    span.brand-color Codificación Municipio (Matamoros)
                  template(#head(rate_saltillo)="data")
                    span.brand-color Codificación Municipio (Saltillo)
                  template(#head(score_torreon)="data")
                    span.brand-color Calificación Rubro (Torreón)
                  template(#head(score_matamoros)="data")
                    span.brand-color Calificación Rubro (Matamoros)
                  template(#head(score_saltillo)="data")
                    span.brand-color Calificación Rubro (Saltillo)

              b-tab(title='Participación Ciudadana')
                p I&apos;m the second tab
              b-tab(title='Rendición de Cuentas')
                p I&apos;m the tab with the very, very long title
              b-tab(title='Rendimiento')
                p I&apos;m the tab with the very, very long title


        //b-row(align-v="center" style="background: darkslategray; border-radius:10px; margin-bottom:50px")
          b-col(md="3")
            a(v-b-modal.modal-1)
              b-img(
                fluid
                center
                src="@/assets/images/Final-1-Coahuila.png"
                alt="Responsive image"
              )
          b-col(md="3")
            a(v-b-modal.modal-1)
              b-img(
                fluid
                center
                src="@/assets/images/Final-1-Coahuila.png"
                alt="Responsive image"
              )
          b-col(md="3")
            a(v-b-modal.modal-1)
              b-img(
                fluid
                center
                src="@/assets/images/Final-1-Coahuila.png"
                alt="Responsive image"
              )
          b-col(md="3")
            a(v-b-modal.modal-1)
              b-img(
                fluid
                center
                src="@/assets/images/Final-1-Coahuila.png"
                alt="Responsive image"
              )
        //b-row(align-v="center")
          b-col(md="4")
            b-form-group(
              id="input-group-short"
              label="Municipio:"
              label-for="input-short"
            )
              b-form-select
                b-form-select-option Todos
                b-form-select-option Torreón
                b-form-select-option Saltillo
                b-form-select-option Matamoros
                b-form-select-option Monclova
          b-col(md="4")
            b-form-group(
              id="input-group-short"
              label="Filtro por nombre:"
              label-for="input-short"
            )
              b-form-input(
                id="input-short"
                type="text"
                placeholder="Ingresa texto para filtrar"
                required
              )

          b-col(md="4")
            b-form-group(
              id="input-group-short"
              label="ASC / DESC:"
              label-for="input-short"
            )
              b-form-select
                b-form-select-option ASCENDENTE
                b-form-select-option DESCENDENTE
          b-col(md="12")
            b-table(hover responsive striped :items="measurements" style="background:white;")

    //Contact
    section#contacto.p-5
      .container
        b-row(align-v="center" )
          b-col(md="6")
            .text-left(style="margin-bottom:10px")
              strong.title Contacto
            .text-left.text-container
              p Si tienes dudas, inquietudes, preguntas, comentarios o sugerencias, llena el siguiente formato y te responderemos a la brevedad.
              p(style="font-size:.9em")
                strong Correo: &ensp;
                a(href="mailto:contacto@ccilaguna.org.mx") contacto@ccilaguna.org.mx
            b-form
              b-form-group(
                id="input-group-email"
                label="Dirección de E-mail:"
                label-for="input-email"
                description="No compartiremos tu información con nadie más."
              )
                b-form-input(
                  id="input-email"
                  type="email"
                  placeholder="Ingresa tu dirección de e-mail"
                  required
                )
              b-form-group(
                id="input-group-message"
                label="Mensaje:"
                label-for="input-message"
                description="No compartiremos tu información con nadie más."
              )
                b-form-textarea(
                  id="input-message"
                  placeholder="Ingresa tu mensaje"
                  required
                )
            b-button(block variant="primary" ) Enviar
          b-col(md="6")
            .google-map
              iframe(
                frameborder="0"
                style="border:0;height: 410px;width:100%"
                src="https://www.google.com/maps/embed/v1/place?q=Bosque%20Venustiano%20Carranza&key=AIzaSyCZI5F_k6S1k46ujh0SNrapM89f7mJxd30"
                allowfullscreen
              )


    //Documents
    section#documentos.p-5(style="background: ghostwhite")
      .container
        b-row(align-v="center")
          b-col(md="12")
            .text-left(style="margin-bottom:10px")
              strong.title Documentos
            .text-left.text-container
              p Sin datos por el momento.
          b-col(md="12")
            //b-table(hover responsive striped :items="documents.items" style="background:white;")
              template(v-slot:head(title)="data")
                strong Título
              template(v-slot:head(text)="data")
                strong Descripción
              template(v-slot:head(href)="data")
                strong Acciones

              template(v-slot:cell(title)="data")
                strong {{ data.item.title }}

              template(v-slot:cell(href)="data")
                b-button(block variant="primary" ) Ver

    //patreons
    section#patrocinadores.p-5
      .container
        b-row(align-v="center" )
          b-col(md="6")
            .text-left(style="margin-bottom:10px")
              //strong.title Patrocinador
            .text-left.text-container
              //p Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor.
        b-row(align-v="center" )
          b-col(md="4" offset-md="4")
            b-img(
              fluid
              center
              src="@/assets/images/logo.png"
              alt="Responsive image"
            )
</template>

<script>

export default {
  name: 'Landing',
  components: {},
  data: function () {
    return {
      measurements: {
          transparency:{
            items:[
              {
                entry: 'Sitio Web',
                question: "Pregunta",
                information_torreon: "http://www.torreon.gob.mx/transparencia/ y http://www.torreon.gob.mx/contraloria",
                information_matamoros: "No cuenta con micrositio",
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 0,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
            ]
          },
      },
      documents: {
        items: [
          {
            title: 'Documento 1',
            text: 'Lorem ipsum dolor sit amet. Curabitur quis vehicula tortorCurabitur quis vehicula tortor . ',
            href: '#'
          },
          {
            title: 'Documento 2',
            text: 'Lorem ipsum dolor sit amet. Curabitur quis vehicula tortorCurabitur quis vehicula tortor . ',
            href: '#'
          },
          {
            title: 'Documento 3',
            text: 'Lorem ipsum dolor sit amet. Curabitur quis vehicula tortorCurabitur quis vehicula tortor . ',
            href: '#'
          },
          {
            title: 'Documento 4',
            text: 'Lorem ipsum dolor sit amet. Curabitur quis vehicula tortorCurabitur quis vehicula tortor . ',
            href: '#'
          },
        ]
      }
    }
  },
}
</script>

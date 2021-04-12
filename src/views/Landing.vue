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
              p Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed bibendum urna erat, et ultrices ex varius in. Curabitur quis vehicula tortor.
              p Phasellus sed porttitor nibh. Suspendisse nunc enim, fringilla sit amet mauris at, malesuada hendrerit odio. consectetur nulla commodo ut. Fusce ornare dolor ut mi lobortis auctor. Morbi pharetra, sapien et pharetra
          b-col(md="6")
            b-img(
              style="width:100%"
              rounded
              src="@/assets/images/quienessomos.jpg"
              alt="Responsive image"
            )


    //Tables
    b-modal(id="modal-1" title="Resultados")
      b-img(
        fluid
        center
        src="@/assets/images/resultados.png"
        alt="Responsive image"
      )
    section#mediciones.p-5(style="background: ghostwhite")
      .container
        b-row(align-v="center")
          b-col(md="12")
            .text-left(style="margin-bottom:10px")
              strong.title Mediciones en Coahuila
            .text-left.text-container
              p Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula.
        b-row(align-v="center" style="background: darkslategray; border-radius:10px; margin-bottom:50px")
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
        b-row(align-v="center")
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
              p Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor.
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
              p Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula.
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
                b-button(block variant="primary" ) Ver

    //patreons
    section#patrocinadores.p-5
      .container
        b-row(align-v="center" )
          b-col(md="6")
            .text-left(style="margin-bottom:10px")
              strong.title Patrocinadores
            .text-left.text-container
              p Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor.
        b-row(align-v="center" )
          b-col(md="3" v-for="(n,k) in 4" :key="k")
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
      measurements: [
        {
          id: '1',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
        {
          id: '2',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
        {
          _rowVariant: 'danger',
          id: '3',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
        {
          _rowVariant: 'warning',
          id: '4',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
        {
          _rowVariant: 'danger',
          id: '5',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
        {
          id: '5',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
        {
          id: '5',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
        {
          _rowVariant: 'danger',
          id: '6',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
        {
          _rowVariant: 'info',
          id: '6',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
        {
          _rowVariant: 'info',
          id: '6',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
        {
          id: '6',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
        {
          _rowVariant: 'success',
          id: '6',
          amet_value: '800',
          lorem_value: 'Dickerson',
          sit_value: '3000pz',
          ipsum_value: 'Macdonald',
          dolor_value: '$1,000.00'
        },
      ],
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

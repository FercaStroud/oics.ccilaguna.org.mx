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
                  template(#thead-top="data")
                    b-tr
                    b-th()
                    b-th()
                    b-th(colspan="3" variant="warning") Información Municipio
                    b-th(colspan="3" variant="success") Codificación Municipio
                    b-th(colspan="3" variant="primary") Calificación Municipio

                  template(#head(entry)="data")
                    .table-info Rubro
                  template(#head(question)="data")
                    .table-danger Pregunta
                  template(#head(information_torreon)="data")
                    .table-warning Torreón
                  template(#head(information_matamoros)="data")
                    .table-warning Matamoros
                  template(#head(information_saltillo)="data")
                    .table-warning Saltillo
                  template(#head(rate_torreon)="data")
                    .table-success Torreón
                  template(#head(rate_matamoros)="data")
                    .table-success Matamoros
                  template(#head(rate_saltillo)="data")
                    .table-success Saltillo
                  template(#head(score_torreon)="data")
                    .table-primary Torreón
                  template(#head(score_matamoros)="data")
                    .table-primary Matamoros
                  template(#head(score_saltillo)="data")
                    .table-primary Saltillo

                  template(#cell(information_torreon)="data")
                    div(v-if="data.value === 'links_torreon'")
                      a(target="_blank" href="http://www.torreon.gob.mx/transparencia/") Transparencia
                      br/
                      a(target="_blank" href="http://www.torreon.gob.mx/contraloria/") Contraloría
                    span(v-else) {{data.value}}
              b-tab(title='Participación Ciudadana')
                b-table(responsive striped :items="measurements.participation.items")
                  template(#thead-top="data")
                    b-tr
                    b-th()
                    b-th()
                    b-th(colspan="3" variant="warning") Información Municipio
                    b-th(colspan="3" variant="success") Codificación Municipio
                    b-th(colspan="3" variant="primary") Calificación Municipio

                  template(#head(entry)="data")
                    .table-info Rubro
                  template(#head(question)="data")
                    .table-danger Pregunta
                  template(#head(information_torreon)="data")
                    .table-warning Torreón
                  template(#head(information_matamoros)="data")
                    .table-warning Matamoros
                  template(#head(information_saltillo)="data")
                    .table-warning Saltillo
                  template(#head(rate_torreon)="data")
                    .table-success Torreón
                  template(#head(rate_matamoros)="data")
                    .table-success Matamoros
                  template(#head(rate_saltillo)="data")
                    .table-success Saltillo
                  template(#head(score_torreon)="data")
                    .table-primary Torreón
                  template(#head(score_matamoros)="data")
                    .table-primary Matamoros
                  template(#head(score_saltillo)="data")
                    .table-primary Saltillo

                  template(#cell(information_torreon)="data")
                    div(v-if="data.value === 'mail'")
                      a(target="_blank" href="mailto:denuncia.contraloria.trc@torreon.gob.mx") E-Mail
                    span(v-else) {{data.value}}

                  template(#cell(information_matamoros)="data")
                    div(v-if="data.value === 'page'")
                      a(target="_blank" href="https://www.matamoroscoahuila.gob.mx/transparencia/quejas.php") Quejas
                    span(v-else) {{data.value}}

              b-tab(title='Rendición de Cuentas')
              b-tab(title='Rendimiento')
                p SIN DATOS


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
                question: "Enlace / URL",
                information_torreon: "links_torreon",
                information_matamoros: "No cuenta con micrositio",
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 0,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Sitio Web',
                question: "Actualización de medios digitales",
                information_torreon: "Trimestral",
                information_matamoros: "Semanal",
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 10,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Sitio Web',
                question: "Información por secciones, vinculos o pestañas / Motores de busqueda",
                information_torreon: "Sí",
                information_matamoros: "No",
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 0,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Sitio Web',
                question: "Motores de búsqueda",
                information_torreon: "Sí",
                information_matamoros: "No",
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 0,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Sitio Web',
                question: "Enlaces hacía sitios de intéres",
                information_torreon: "Sí",
                information_matamoros: "No",
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 0,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Sitio Web',
                question: "Instrumentos de intercambio con la ciudadanía",
                information_torreon: "Sí",
                information_matamoros: "No",
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 0,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Sitio Web',
                question: "Documentos de auditoría",
                information_torreon: "No",
                information_matamoros: "No",
                information_saltillo: "",
                rate_torreon: 0,
                rate_matamoros: 0,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Sitio Web',
                question: "Información institucional",
                information_torreon: "Sí",
                information_matamoros: "Sí",
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 10,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Sitio Web',
                question: "Documentos de gestión",
                information_torreon: "Sí",
                information_matamoros: "Sí",
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 10,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Sitio Web',
                question: "Descarga de contenido",
                information_torreon: "Sí",
                information_matamoros: "No",
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 0,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Disponibilidad y Calidad de la Información Relevante',
                question: "Reglamento interior descargable",
                information_torreon: "Sí",
                information_matamoros: 0,
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 10,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Disponibilidad y Calidad de la Información Relevante',
                question: "Organigrama de la contraloría",
                information_torreon: "Sí",
                information_matamoros: "Sí",
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 10,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Disponibilidad y Calidad de la Información Relevante',
                question: "Actividades de la contraloría",
                information_torreon: "Sí",
                information_matamoros: 0,
                information_saltillo: "",
                rate_torreon: 10,
                rate_matamoros: 10,
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Disponibilidad y Calidad de la Información Relevante',
                question: "Contiene el cronograma de auditorías",
                information_torreon: "",
                information_matamoros: "",
                information_saltillo: "",
                rate_torreon: "",
                rate_matamoros: "",
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Disponibilidad y Calidad de la Información Relevante',
                question: "Informes de las auditorías aplicadas por la contraloría",
                information_torreon: "",
                information_matamoros: "",
                information_saltillo: "",
                rate_torreon: "",
                rate_matamoros: "",
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Disponibilidad y Calidad de la Información Relevante',
                question: "Descarga los informes de auditoría",
                information_torreon: "",
                information_matamoros: "",
                information_saltillo: "",
                rate_torreon: "",
                rate_matamoros: "",
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Disponibilidad y Calidad de la Información Relevante',
                question: "Presupuesto asignado a la contraloría",
                information_torreon: "",
                information_matamoros: "",
                information_saltillo: "",
                rate_torreon: "",
                rate_matamoros: "",
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Disponibilidad y Calidad de la Información Relevante',
                question: "Desglosa los bienes y/o servicios contratados por la contraloría",
                information_torreon: "",
                information_matamoros: "",
                information_saltillo: "",
                rate_torreon: "",
                rate_matamoros: "",
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
              {
                entry: 'Disponibilidad y Calidad de la Información Relevante',
                question: "Descarga la información de servicios",
                information_torreon: "",
                information_matamoros: "",
                information_saltillo: "",
                rate_torreon: "",
                rate_matamoros: "",
                rate_saltillo: "",
                score_torreon: "",
                score_matamoros: "",
                score_saltillo: "",
              },
            ]
        },
        participation:{
          items:[
            {
              entry: 'Quejas y denuncias',
              question: "Quejas/denuncias en el portal del OIC",
              information_torreon: "Trimestral",
              information_matamoros: "No contestó",
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 0,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Quejas y denuncias',
              question: "Unidad de Atención para quejas/denuncias",
              information_torreon: "Sí",
              information_matamoros: "Sí",
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Quejas y denuncias',
              question: "Intervenciónn directa o indirecta de sociedad civil en auditorias",
              information_torreon: "No",
              information_matamoros: "No",
              information_saltillo: "",
              rate_torreon: 0,
              rate_matamoros: 0,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Quejas y denuncias',
              question: "Intervenciónn directa o indirecta de sociedad civil en auditorias",
              information_torreon: 4,
              information_matamoros: 3,
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 7.5,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Quejas y denuncias',
              question: "Buzón de quejas /denuncia",
              information_torreon: "mail",
              information_matamoros: "page",
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Lineamientos del Sistema Estatal Anticorrupción',
              question: "Intercambio de informacion entre el SEA y el OIC",
              information_torreon: "Otro",
              information_matamoros: "No contestó",
              information_saltillo: "",
              rate_torreon: 5,
              rate_matamoros: 0,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Lineamientos del Sistema Estatal Anticorrupción',
              question: "SEA ha notificado al OIC sobre lineamientos emitidos",
              information_torreon: "No",
              information_matamoros: "Sí",
              information_saltillo: "",
              rate_torreon: 0,
              rate_matamoros: 10,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Lineamientos del Sistema Estatal Anticorrupción',
              question: "Marco legal esta homogolado con las reformas federales",
              information_torreon: 4,
              information_matamoros: 3,
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 7.5,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Perfil Contralor',
              question: "Marco legal para designar al contralor esta homogolado con las reformas federales",
              information_torreon: 2,
              information_matamoros: 1,
              information_saltillo: "",
              rate_torreon: 5,
              rate_matamoros: 2.5,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Perfil Contralor',
              question: "Homogeneidad en la designación para ser contalor con el Codigo Municipal y Reglamento Interior",
              information_torreon: "No",
              information_matamoros: "Sí",
              information_saltillo: "",
              rate_torreon: 0,
              rate_matamoros: 10,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Perfil Contralor',
              question: "Forma de designación del OIC",
              information_torreon: "Otra",
              information_matamoros: "Otra",
              information_saltillo: "",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Perfil Contralor',
              question: "Evaluaciones del contralor están publicadas en la pagina oficial",
              information_torreon: 2,
              information_matamoros: 1,
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Convocatoria pública al cargo de contralor',
              question: "Marco legal para emitir la convocatoria pública para designar al contralor esta homogolado con las reformas federales",
              information_torreon: 1,
              information_matamoros: 1,
              information_saltillo: "",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Convocatoria pública al cargo de contralor',
              question: "Existen lineamientos para emitir y llevar a cabo la convocatoria pública al cargo de contralor",
              information_torreon: "Sí",
              information_matamoros: "Sí",
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Convocatoria pública al cargo de contralor',
              question: "Plataforma digital para emitir la convocatoria pública al cargo de contralor",
              information_torreon: "No",
              information_matamoros: "Sí",
              information_saltillo: "",
              rate_torreon: 0,
              rate_matamoros: 10,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Convocatoria pública al cargo de contralor',
              question: "Intervención directa de la ciudadanía con voz y voto en ",
              information_torreon: 0,
              information_matamoros: 1,
              information_saltillo: "",
              rate_torreon: 0,
              rate_matamoros: 5,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Contraloría Social',
              question: "Participación ciudadana en la Contraloría Municipal",
              information_torreon: "Sí",
              information_matamoros: "No",
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 0,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Contraloría Social',
              question: "Mecanismo de participación ciudadana en la Contraloría Municipal",
              information_torreon: "Reuniones de evaluación de las obras realizadas en éscuelas de educacion primaria, por medio de un programa social ya sea de fondos municipales, estatales o federales.",
              information_matamoros: "Comité de contraloría social",
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Contraloría Social',
              question: "Normatividad para regular la participacion ciudadana en la Contraloria Social",
              information_torreon: "Sí",
              information_matamoros: "No",
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 0,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Contraloría Social',
              question: "Normatividad que regula la participación ciudadana en la Contraloría Social",
              information_torreon: "Ley de desarrollo social art 6",
              information_matamoros: "Ley de desarrollo social art 6",
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
            {
              entry: 'Contraloría Social',
              question: "Participación ciudadana",
              information_torreon: 1,
              information_matamoros: 1,
              information_saltillo: "",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: "",
              score_torreon: "",
              score_matamoros: "",
              score_saltillo: "",
            },
          ]
        }
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

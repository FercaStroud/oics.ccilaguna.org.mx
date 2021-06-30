<template lang="pug">
  section#mediciones.p-5(style="background: ghostwhite")
    .container
      b-row(align-v="center")
        b-col(md="12")
          .text-left(style="margin-bottom:10px")
            strong.title Indicadores por Municipio
          .text-left.text-container
            //p Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula tortor. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur quis vehicula.
      b-row(align-v="center")
        b-col
          .text-left.text-container Filtrar por municipio:
      b-row(align-v="center" style="margin-top:20px")
        b-col(sm="4" md="4")
          img.municipality-img(
            @click="handlerCity('torreon', filters.torreon)"
            style="cursor:pointer; width:100%;" src="@/assets/images/mapa_torreon.png"
          )
          .score-title(v-if="selectedEntry !== ''" style="color: #004786") Calificación por Rubro
          .score-container(style="color: #00aed2") {{ selectedEntry.score_torreon }}
          .municipality-container(style="color: #004786")
            font-awesome-icon(
              v-if="filters.torreon"
              :icon="['fas', 'toggle-on']"
              style="color:#004786;margin-right:5px"
              @click="handlerCity('torreon', filters.torreon)"
            )
            font-awesome-icon(
              v-else
              @click="handlerCity('torreon', filters.torreon)"
              :icon="['fas', 'toggle-off']"
              style="color:#acacac;margin-right:5px"
            )
            strong(@click="handlerCity('torreon', filters.torreon)" style="font-size:1.2em;") Torreón

        b-col(sm="4" md="4")
          img.municipality-img(
            @click="handlerCity('matamoros', filters.matamoros)"
            style="cursor:pointer; width:100%;" src="@/assets/images/mapa_matamoros.png"
          )
          .score-title(v-if="selectedEntry !== ''" style="color: #004786") Calificación por Rubro
          .score-container(style="color: #ff34b0") {{ selectedEntry.score_matamoros }}
          .municipality-container(style="color: #004786")
            font-awesome-icon(
              @click="handlerCity('matamoros', filters.matamoros)"
              v-if="filters.matamoros"
              :icon="['fas', 'toggle-on']"
              style="color:#004786;margin-right:5px"
            )
            font-awesome-icon(
              v-else
              @click="handlerCity('matamoros', filters.matamoros)"
              :icon="['fas', 'toggle-off']"
              style="color:#acacac;margin-right:5px"
            )
            strong(@click="handlerCity('matamoros', filters.matamoros)" style="font-size:1.2em;") Matamoros

        b-col(sm="4" md="4")
          img.municipality-img(
            @click="handlerCity('saltillo', filters.saltillo)"
            style="cursor:pointer; width:100%;" src="@/assets/images/mapa_saltillo.png"
          )
          .score-title(v-if="selectedEntry !== ''" style="color: #004786") Calificación por Rubro
          .score-container(style="color: #004786") {{ selectedEntry.score_saltillo }}
          .municipality-container(style="color: #004786")
            font-awesome-icon(
              @click="handlerCity('saltillo', filters.saltillo)"
              v-if="filters.saltillo"
              :icon="['fas', 'toggle-on']"
              style="color:#004786;margin-right:5px"
            )
            font-awesome-icon(
              v-else
              @click="handlerCity('saltillo', filters.saltillo)"
              :icon="['fas', 'toggle-off']"
              style="color:#acacac;margin-right:5px"
            )
            strong(@click="handlerCity('saltillo', filters.saltillo)" style="font-size:1.2em;") Saltillo


      b-row(align-v="center" style="margin-top:20px")
        b-col(md="12")
          div(style="text-align: left;:left; width:100%;margin-top:10px") Eje
          b-form-select(
            v-model="selectedMeasurement"
            @change="onChangeMeasurement"
          )
            b-form-select-option-group(
              label='Filtro de Selección de Eje'
            )
              b-form-select-option(
                v-for="(measurement, key) in measurements"
                :key="key"
                :value="measurement"
              ) {{ measurement.title }}

        b-col(md="6")
          div(style="text-align: left;:left; width:100%;margin-top:10px") Rubro
          b-form-select(
            v-model="selectedEntry"
            @change="onChangeEntry"
          )
            b-form-select-option-group(label='Filtro de Selección de Rubro')
              b-form-select-option(
                v-for="(entry, key) in selectedMeasurement.entries"
                :key="key"
                :value="entry"
              ) {{ entry.title }}

        b-col(md="6")
          div(style="text-align: left;:left; width:100%;margin-top:10px") Indicadores
          b-form-select(
            v-model="selectedQuestion"
            @change="onChangeQuestion"
          )
            b-form-select-option-group(label='Filtro de Selección de Indicador')
              b-form-select-option(
                v-for="(question, key) in selectedEntry.questions"
                :key="key"
                :value="question"
              ) {{ question.title }}


      b-row(v-if="!filters.torreon && !filters.matamoros && !filters.saltillo" align-v="center" style="margin-top:20px")
        strong.text-danger Seleccione un municipio para visualizar datos.
      b-row(align-v="center" style="margin-top:20px")
        b-col(sm="12" md="6")
          strong {{ selectedMeasurement.title }}
          p {{ selectedMeasurement.description }}
          strong {{ selectedEntry.title }}
          p {{ selectedEntry.description }}
          strong {{ selectedQuestion.title }}
          p {{ selectedQuestion.description }}
        b-col(sm="12" md="6")
          bar-chart(
            :rates="rates"
            :labels="labels"
            v-if="barChart"
          )

</template>

<script>
import BarChart from "../components/BarChart";

export default {
  components: {BarChart},
  name: "Measurements",
  data: function () {
    return {
      barChart:false,
      labels: [],
      rates: [],
      selectedMeasurement: '',
      selectedEntry: '',
      selectedQuestion: '',
      filters: {
        saltillo: false,
        torreon: true,
        matamoros: false,
      },
      measurements: {
        transparency: {
          title: 'Transparencia y Rendición de Cuentas',
          description: 'La transparencia hace referencia a la disponibilidad de información a través de la cual el OIC hace visibles y accesibles -de manera suficiente, oportuna, clara y adecuada sus acciones, políticas, procedimientos y decisiones.',
          items: [
            {
              entry: 'Sitio Web',
              question: "Enlace / URL",
              //information_torreon: "links_torreon",
              information_torreon: "Sí, hay micrositio pero no se encuentra en los motores de búsqueda (no está indexado) y no hay un vínculo en el ayuntamiento que nos redirija al micrositio.",
              information_matamoros: "No cuenta con micrositio",
              information_saltillo: "Sí.",
              rate_torreon: 8,
              rate_matamoros: 5,
              rate_saltillo: 10,
              score_torreon: "8.2",
              score_matamoros: "6.3",
              score_saltillo: "9.6",
            },
            {
              entry: 'Sitio Web',
              question: "Actualización de medios digitales",
              information_torreon: "Trimestral",
              information_matamoros: "Semanal (página web)",
              information_saltillo: "Semanal",
              rate_torreon: 8,
              rate_matamoros: 8,
              rate_saltillo: 8,
              score_torreon: "8.2",
              score_matamoros: "6.3",
              score_saltillo: "9.6",
            },
            {
              entry: 'Sitio Web',
              question: "Información por secciones, vinculos o pestañas / Motores de busqueda",
              information_torreon: "Sí. Faltan motores de búsqueda, no hay enlaces a sitios de interés.",
              information_matamoros: "No",
              information_saltillo: "Sí, disponen de motores de búsqueda y enlaces a sitios de interés.",
              rate_torreon: 8,
              rate_matamoros: 5,
              rate_saltillo: 10,
              score_torreon: "8.2",
              score_matamoros: "6.3",
              score_saltillo: "9.6",
            },
            {
              entry: 'Sitio Web',
              question: "Motores de búsqueda",
              information_torreon: "No",
              information_matamoros: "No",
              information_saltillo: "Sí",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: 10,
              score_torreon: "8.2",
              score_matamoros: "6.3",
              score_saltillo: "9.6",
            },
            {
              entry: 'Sitio Web',
              question: "Enlaces hacía sitios de intéres",
              information_torreon: "No",
              information_matamoros: "No",
              information_saltillo: "Sí",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: 9,
              score_torreon: "8.2",
              score_matamoros: "6.3",
              score_saltillo: "9.6",
            },
            {
              entry: 'Sitio Web',
              question: "Instrumentos de intercambio con la ciudadanía",
              information_torreon: "Sí",
              information_matamoros: "No",
              information_saltillo: "Sí",
              rate_torreon: 10,
              rate_matamoros: 5,
              rate_saltillo: 10,
              score_torreon: "8.2",
              score_matamoros: "6.3",
              score_saltillo: "9.6",
            },
            {
              entry: 'Sitio Web',
              question: "Documentos de auditoría",
              information_torreon: "Sí, pero los documentos están en Transparencia no en el micrositio de la Contraloría.",
              information_matamoros: "No",
              information_saltillo: "Sí, el cronograma está en el micrositio pero los informes están en el portal de transparencia.",
              rate_torreon: 8,
              rate_matamoros: 5,
              rate_saltillo: 9,
              score_torreon: "8.2",
              score_matamoros: "6.3",
              score_saltillo: "9.6",
            },
            {
              entry: 'Sitio Web',
              question: "Información institucional",
              information_torreon: "Sí",
              information_matamoros: "Sí",
              information_saltillo: "Sí",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: 10,
              score_torreon: "8.2",
              score_matamoros: "6.3",
              score_saltillo: "9.6",
            },
            {
              entry: 'Sitio Web',
              question: "Documentos de gestión",
              information_torreon: "Sí, existen vínculos en el micrositio y éstos te redirigen a otro portal.",
              information_matamoros: "Sí",
              information_saltillo: "Sí, los documentos de gestión se encuentra en el micrositio (formatos de padrón de proveedores, normatividad).",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: 10,
              score_torreon: "8.2",
              score_matamoros: "6.3",
              score_saltillo: "9.6",
            },
            {
              entry: 'Sitio Web',
              question: "Descarga de contenido",
              information_torreon: "Sí",
              information_matamoros: "No",
              information_saltillo: "Sí",
              rate_torreon: 10,
              rate_matamoros: 5,
              rate_saltillo: 10,
              score_torreon: "8.2",
              score_matamoros: "6.3",
              score_saltillo: "9.6",
            },
            {
              entry: 'Disponibilidad y Calidad de la Información Relevante',
              question: "Reglamento interior descargable",
              information_torreon: "Sí",
              information_matamoros: 0,
              information_saltillo: "Sí",
              rate_torreon: 10,
              rate_matamoros: 5,
              rate_saltillo: 10,
              score_torreon: "6.8",
              score_matamoros: "5.6",
              score_saltillo: "7.8",
            },
            {
              entry: 'Disponibilidad y Calidad de la Información Relevante',
              question: "Organigrama de la contraloría",
              information_torreon: "Sí",
              information_matamoros: "Sí",
              information_saltillo: "Sí",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: 10,
              score_torreon: "6.8",
              score_matamoros: "5.6",
              score_saltillo: "7.8",
            },
            {
              entry: 'Disponibilidad y Calidad de la Información Relevante',
              question: "Actividades de la contraloría",
              information_torreon: "Sí. No tiene publicados los informes de auditoría.",
              information_matamoros: 0,
              information_saltillo: "Sí",
              rate_torreon: 8,
              rate_matamoros: 5,
              rate_saltillo: 10,
              score_torreon: "6.8",
              score_matamoros: "5.6",
              score_saltillo: "7.8",
            },
            {
              entry: 'Disponibilidad y Calidad de la Información Relevante',
              question: "Contiene el cronograma de auditorías",
              information_torreon: "No. Se recomienda que se publique el cronograma de auditorías en el micrositio.",
              information_matamoros: "",
              information_saltillo: "Sí",
              rate_torreon: 8,
              rate_matamoros: 5,
              rate_saltillo: 10,
              score_torreon: "6.8",
              score_matamoros: "5.6",
              score_saltillo: "7.8",
            },
            {
              entry: 'Disponibilidad y Calidad de la Información Relevante',
              question: "Informes de las auditorías aplicadas por la contraloría",
              information_torreon: "No",
              information_matamoros: "",
              information_saltillo: "No (En el apartado de transparencia sólo se cuenta con el número, tipo y los resultados de las auditorías practicadas).",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: 7,
              score_torreon: "6.8",
              score_matamoros: "5.6",
              score_saltillo: "7.8",
            },
            {
              entry: 'Disponibilidad y Calidad de la Información Relevante',
              question: "Descarga los informes de auditoría",
              information_torreon: "No (En el apartado de transparencia sólo se cuenta con el número, tipo y los resultados de las auditorías practicadas).",
              information_matamoros: "",
              information_saltillo: "No (En el apartado de transparencia sólo se cuenta con el número, tipo y los resultados de las auditorías practicadas).",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: 5,
              score_torreon: "6.8",
              score_matamoros: "5.6",
              score_saltillo: "7.8",
            },
            {
              entry: 'Disponibilidad y Calidad de la Información Relevante',
              question: "Presupuesto asignado a la contraloría",
              information_torreon: "Sí, pero tanto la información del presupuesto aprobado así como del ejercido vienen únicamente en la Información Pública de Oficio del apartado de Transparencia, sin embargo no hay un desglose por concepto para la Contraloría en el presupuesto aprobado, y en el ejercido no hay desglose por capítulo ni concepto.",
              information_matamoros: "",
              information_saltillo: "Sí, pero tanto la información del presupuesto aprobado así como del ejercido vienen únicamente en la Información Pública de Oficio del apartado de Transparencia, sin embargo no hay un desglose por concepto para la Contraloría en el presupuesto aprobado, y en el ejercido no hay desglose por capítulo ni concepto.",
              rate_torreon: 8,
              rate_matamoros: 5,
              rate_saltillo: 8,
              score_torreon: "6.8",
              score_matamoros: "5.6",
              score_saltillo: "7.8",
            },
            {
              entry: 'Disponibilidad y Calidad de la Información Relevante',
              question: "Desglosa los bienes y/o servicios contratados por la contraloría",
              information_torreon: "No",
              information_matamoros: "",
              information_saltillo: "No",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: 5,
              score_torreon: "6.8",
              score_matamoros: "5.6",
              score_saltillo: "7.8",
            },
            {
              entry: 'Disponibilidad y Calidad de la Información Relevante',
              question: "Descarga la información de servicios",
              information_torreon: "No",
              information_matamoros: "",
              information_saltillo: "No",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: 5,
              score_torreon: "6.8",
              score_matamoros: "5.6",
              score_saltillo: "7.8",
            },
          ],
          entries: [
            {
              title: '',
              description: '',
            },
            {
              title: 'Sitio Web',
              description: 'El sitio Web es un instrumento de comunicación y de enlace entre cualquier organismo público, y como tal es una plataforma a través de la cual el organismo puede cumplir con altos estándares de transparencia activa.',
              score_torreon: 8.2,
              score_matamoros: 6.3,
              score_saltillo: 9.6,
              questions: [
                {
                  title: '',
                  description: ''
                },
                {
                  title: 'Enlace / URL',
                  description: 'Corresponde al sitio web del OIC',
                  rate_torreon: 8,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Actualización de medios digitales',
                  description: '',
                  rate_torreon: 8,
                  rate_matamoros: 5,
                  rate_saltillo: 8,
                },
                {
                  title: 'Información por secciones, vinculos o pestañas / Motores de busqueda',
                  description: ''
                },
                {
                  title: 'Motores de búsqueda',
                  description: ''
                },
                {
                  title: 'Enlaces hacía sitios de intéres',
                  description: ''
                },
                {
                  title: 'Instrumentos de intercambio con la ciudadanía',
                  description: ''
                },
                {
                  title: 'Documentos de auditoría',
                  description: ''
                },
                {
                  title: 'Información institucional',
                  description: ''
                },
                {
                  title: 'Documentos de gestión',
                  description: ''
                },
                {
                  title: 'Descarga de contenido',
                  description: ''
                }
              ]
            },
            {
              title: 'Disponibilidad y Calidad de la Información Relevante',
              description: 'La información relevante de la entidad hace referencia a datos y contenidos informativos sobre la identidad de la institución fiscalizadora y su funcionamiento interno.',
              score_torreon: "6.8",
              score_matamoros: "5.6",
              score_saltillo: "7.8",
              questions: [
                {
                  title: '',
                  description: ''
                },
                {
                  title: 'Reglamento interior descargable',
                  description: '',
                },
                {
                  title: 'Organigrama de la contraloría',
                  description: '',
                },
                {
                  title: 'Actividades de la contraloría',
                  description: '',
                },
                {
                  title: 'Contiene el cronograma de auditorías',
                  description: '',
                },
                {
                  title: 'Informes de las auditorías aplicadas por la contraloría',
                  description: '',
                },
                {
                  title: 'Descarga los informes de auditoría',
                  description: '',
                },
                {
                  title: 'Presupuesto asignado a la contraloría',
                  description: '',
                },
                {
                  title: 'Desglosa los bienes y/o servicios contratados por la contraloría',
                  description: '',
                },
                {
                  title: 'Descarga la información de servicios',
                  description: '',
                },
              ]
            }
          ]
        },
        participation: {
          title: 'Participación Ciudadana',
          description: 'Se refiere a la dimensión de apertura del OIC para incorporar mecanismos e instancias de cooperación y de articulación que faciliten el ejercicio de un control activo por parte de los ciudadanos y organizaciones de la sociedad civil. Es imprescindible garantizar la participación de la ciudadanía a fin de perfeccionar la calidad del control, y su involucramiento coadyuva a una mayor cultura de transparencia gubernamental.',
          items: [
            {
              entry: 'Quejas y denuncias',
              question: "Quejas/denuncias en el portal del OIC",
              information_torreon: "Trimestral. Información actualizada en el portal de Transparencia.",
              information_matamoros: "No contestó",
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 5,
              rate_saltillo: 10,
              score_torreon: "9",
              score_matamoros: "7.5",
              score_saltillo: "7",
            },
            {
              entry: 'Quejas y denuncias',
              question: "Unidad de Atención para quejas/denuncias",
              information_torreon: "Sí",
              information_matamoros: "Sí",
              information_saltillo: "Sí",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: 10,
              score_torreon: "9",
              score_matamoros: "7.5",
              score_saltillo: "7",
            },
            {
              entry: 'Quejas y denuncias',
              question: "Intervención directa o indirecta de sociedad civil en auditorias",
              information_torreon: "No",
              information_matamoros: "No",
              information_saltillo: "No",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: 5,
              score_torreon: "9",
              score_matamoros: "7.5",
              score_saltillo: "7",
            },
            {
              entry: 'Quejas y denuncias',
              question: "Informe  del estado Procesal de la queja",
              information_torreon: 4,
              information_matamoros: 3,
              information_saltillo: "No está el estatus completo, y la información viene para todas las unidades administrativas (no sólo contraloría)  ",
              rate_torreon: 10,
              rate_matamoros: 7.5,
              rate_saltillo: "",
              score_torreon: "9",
              score_matamoros: "7.5",
              score_saltillo: "7",
            },
            {
              entry: 'Quejas y denuncias',
              question: "Buzón de quejas /denuncia",
              information_torreon: "mail",
              information_matamoros: "page",
              information_saltillo: "page",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: 10,
              score_torreon: "9",
              score_matamoros: "7.5",
              score_saltillo: "7",
            },
            {
              entry: 'Lineamientos del Sistema Estatal Anticorrupción',
              question: "Intercambio de informacion entre el SEA y el OIC",
              information_torreon: "",
              information_matamoros: "",
              information_saltillo: "",
              rate_torreon: "",
              rate_matamoros: "",
              rate_saltillo: "",
              score_torreon: "3.3",
              score_matamoros: "2.5",
              score_saltillo: "7",
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
              score_torreon: "3.3",
              score_matamoros: "2.5",
              score_saltillo: "7",
            },
            {
              entry: 'Lineamientos del Sistema Estatal Anticorrupción',
              question: "Marco legal esta homogolado con las reformas federales",
              information_torreon: "2 (Código Municipal y el Manual de Organización)",
              information_matamoros: "1 (Código Municipal)",
              information_saltillo: "2 (Código Municipal y Organización)",
              rate_torreon: 10,
              rate_matamoros: 7.5,
              rate_saltillo: 10,
              score_torreon: "3.3",
              score_matamoros: "2.5",
              score_saltillo: "7",
            },
            {
              entry: 'Perfil Contralor',
              question: "Marco legal para designar al contralor esta homogolado con las reformas federales",
              information_torreon: "Sí",
              information_matamoros: "Sí",
              information_saltillo: "Sí",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: 10,
              score_torreon: "9.4",
              score_matamoros: "8.8",
              score_saltillo: "9.6",
            },
            {
              entry: 'Perfil Contralor',
              question: "Homogeneidad en la designación para ser contalor con el Codigo Municipal y Reglamento Interior",
              information_torreon: "Sí",
              information_matamoros: "Sí",
              information_saltillo: "Sí",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: 10,
              score_torreon: "9.4",
              score_matamoros: "8.8",
              score_saltillo: "9.6",
            },
            {
              entry: 'Perfil Contralor',
              question: "Forma de designación del OIC",
              information_torreon: "Convocatoria",
              information_matamoros: "Convocatoria",
              information_saltillo: "Convocatoria",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: 10,
              score_torreon: "9.4",
              score_matamoros: "8.8",
              score_saltillo: "9.6",
            },
            {
              entry: 'Perfil Contralor',
              question: "Evaluaciones del contralor están publicadas en la pagina oficial",
              information_torreon: 2,
              information_matamoros: 1,
              information_saltillo: 3,
              rate_torreon: 7.5,
              rate_matamoros: 5,
              rate_saltillo: 8.5,
              score_torreon: "9.4",
              score_matamoros: "8.8",
              score_saltillo: "9.6",
            },
            {
              entry: 'Convocatoria pública al cargo de contralor',
              question: "Marco legal para emitir la convocatoria pública para designar al contralor esta homogolado con las reformas federales",
              information_torreon: "1 de 4",
              information_matamoros: "1",
              information_saltillo: "1 de 4",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: 5,
              score_torreon: "5",
              score_matamoros: "7",
              score_saltillo: "5",
            },
            {
              entry: 'Convocatoria pública al cargo de contralor',
              question: "Existen lineamientos para emitir y llevar a cabo la convocatoria pública al cargo de contralor",
              information_torreon: "No",
              information_matamoros: "Sí",
              information_saltillo: "No",
              rate_torreon: 5,
              rate_matamoros: 10,
              rate_saltillo: 5,
              score_torreon: "5",
              score_matamoros: "7",
              score_saltillo: "5",
            },
            {
              entry: 'Convocatoria pública al cargo de contralor',
              question: "Plataforma digital para emitir la convocatoria pública al cargo de contralor",
              information_torreon: "No",
              information_matamoros: "No",
              information_saltillo: "No",
              rate_torreon: 5,
              rate_matamoros: 5,
              rate_saltillo: 5,
              score_torreon: "5",
              score_matamoros: "7",
              score_saltillo: "5",
            },
            {
              entry: 'Convocatoria pública al cargo de contralor',
              question: "Intervención directa de la ciudadanía con voz y voto en ",
              information_torreon: "0 de 4",
              information_matamoros: "1",
              information_saltillo: "0 de 4",
              rate_torreon: 5,
              rate_matamoros: 8,
              rate_saltillo: 5,
              score_torreon: "5",
              score_matamoros: "7",
              score_saltillo: "5",
            },
            {
              entry: 'Contraloría Social',
              question: "Participación ciudadana en la Contraloría Municipal",
              information_torreon: "Sí",
              information_matamoros: "Sí tiene pero no está normado.",
              information_saltillo: "Sí, el manual de procedimiento está en proyecto.",
              rate_torreon: 10,
              rate_matamoros: 8,
              rate_saltillo: 5,
              score_torreon: "10",
              score_matamoros: "8.25",
              score_saltillo: "8.25",
            },
            {
              entry: 'Contraloría Social',
              question: "Mecanismo de participación ciudadana en la Contraloría Municipal",
              information_torreon: "Reuniones de evaluación de las obras realizadas en éscuelas de educacion primaria, por medio de un programa social ya sea de fondos municipales, estatales o federales.",
              information_matamoros: "Comité de contraloría social",
              information_saltillo: "Comisiones Pro Obra y Consejo Ciudadano",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: 10,
              score_torreon: "10",
              score_matamoros: "8.25",
              score_saltillo: "8.25",
            },
            {
              entry: 'Contraloría Social',
              question: "Mecanismo de participación ciudadana en la Contraloría Municipal",
              information_torreon: "Sí",
              information_matamoros: "No",
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 5,
              rate_saltillo: 5,
              score_torreon: "10",
              score_matamoros: "8.25",
              score_saltillo: "8.25",
            },
            /*{
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
            },*/
            {
              entry: 'Contraloría Social',
              question: "Participación ciudadana",
              information_torreon: 1,
              information_matamoros: 1,
              information_saltillo: "",
              rate_torreon: 10,
              rate_matamoros: 10,
              rate_saltillo: 10,
              score_torreon: "10",
              score_matamoros: "8.25",
              score_saltillo: "8.25",
            },
          ],
          entries: [
            {
              title: '',
              description: '',
            },
            {
              title: '',
              description: '',
            },
          ]
        }
      },
    }
  },
  methods: {
    onChangeMeasurement: function () {
      this.selectedEntry = '';
      this.selectedQuestion = '';
    },
    onChangeEntry: function () {
      this.selectedQuestion = '';
    },
    onChangeQuestion: function () {
      this.updateTable();
    },
    updateTable: function () {
      this.barChart = false;
      this.$forceUpdate();

      this.$nextTick(function (){
        let label_torreon = "";
        let label_matamoros = "";
        let label_saltillo = "";

        let rate_torreon = 0;
        let rate_matamoros = 0;
        let rate_saltillo = 0;

        if(this.filters.torreon){
          label_torreon = "Torreón";
          if(this.selectedQuestion.rate_torreon !== undefined){
            rate_torreon = this.selectedQuestion.rate_torreon;
          }
        }
        if(this.filters.matamoros){
          label_matamoros = "Matamoros";
          if(this.selectedQuestion.rate_matamoros !== undefined) {
            rate_matamoros = this.selectedQuestion.rate_matamoros;
          }
        }
        if(this.filters.saltillo){
          label_saltillo = "Saltillo";
          if(this.selectedQuestion.rate_saltillo !== undefined) {
            rate_saltillo = this.selectedQuestion.rate_saltillo;
          }
        }

        this.labels = [label_torreon, label_matamoros, label_saltillo];
        this.rates = [rate_torreon, rate_matamoros, rate_saltillo];

        this.barChart = true;
      });



    },
    handlerCity: function (city, data) {
      switch (city) {
        case 'torreon':
          this.filters.torreon = !data;
          break;
        case 'matamoros':
          this.filters.matamoros = !data;
          break;
        case 'saltillo':
          this.filters.saltillo = !data;
          break;
      }

      this.updateTable();
    }
  }
}
</script>

<style scoped>

</style>

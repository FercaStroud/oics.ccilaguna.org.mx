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
          p(style="text-align:justify !important;")
            strong {{ selectedMeasurement.title }}
          p(style="text-align:justify !important;") {{ selectedMeasurement.description }}
          p(style="text-align:justify !important;")
            strong {{ selectedEntry.title }}
          p(style="text-align:justify !important;") {{ selectedEntry.description }}
          p(style="text-align:justify !important;")
            strong {{ selectedQuestion.title }}
          p(style="text-align:justify !important;") {{ selectedQuestion.description }}
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
          title: 'Transparencia y Acceso a la Información',
          description: 'Construir un buen gobierno implica la apertura de su actuación al escrutinio público a través de mecanismos que garanticen a los ciudadanos accesibilidad total al ejercicio de la función pública e impulsen esquemas de corresponsabilidad en la elaboración de políticas públicas encaminadas a la formación de una conducta ética en el funcionamiento administrativo, transparencia en la asignación y el manejo de recursos públicos, así como la rendición de cuentas de acuerdo a las metas establecidas en el corto, mediano y largo plazos. La transparencia hace referencia a la disponibilidad de información a través de la cual el OIC hace visibles y accesibles -de manera suficiente, oportuna, clara y adecuada sus acciones, políticas, procedimientos y decisiones. El acceso a la información representa un componente central de la transparencia de la entidad, pues constituye el primer eslabón en el proceso de apertura de los organismos a la sociedad civil, y es fundamental para posicionarse como instituciones claves y reconocidas públicamente por la calidad de la labor que desempeñan.',
          entries: [
            {
              title: '',
              description: '',
              score_torreon: 0,
              score_matamoros: 0,
              score_saltillo: 0,
            },
            {
              title: 'Sitio Web',
              description: 'El sitio Web es un instrumento de comunicación y de enlace entre cualquier organismo público, y como tal es una plataforma a través de la cual el organismo puede cumplir con altos estándares de transparencia activa.',
              score_torreon: 8.4,
              score_matamoros: 6,
              score_saltillo: 8.9,
              questions: [
                {
                  title: '',
                  description: ''
                },
                {
                  title: 'Micrositio',
                  description: 'Corresponde al sitio web del OIC',
                  rate_torreon: 8,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Actualización de medios digitales',
                  description: 'Periodicidad con que se actualiza el contenido del Sitio Web.',
                  rate_torreon: 8,
                  rate_matamoros: 5,
                  rate_saltillo: 8,
                },
                {
                  title: 'Información por secciones, vinculos o pestañas / Motores de busqueda',
                  description: 'El contenido del Sitio Web está clasificado por secciones, pestañas o vínculos.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Motores de búsqueda',
                  description: 'Herramientas que facilitan la busqueda de información contenida en el Sitio Web.',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 8,
                },
                {
                  title: 'Enlaces hacía sitios de intéres',
                  description: 'Enlaces hacía trámites de la propia Contraloría Municipal o hacía otros entes fiscalizadores u observadores del gasto público.',
                  rate_torreon: 7,
                  rate_matamoros: 5,
                  rate_saltillo: 7,
                },
                {
                  title: 'Instrumentos de intercambio con la ciudadanía',
                  description: 'Chat en tiempo real, formularios de contacto que permiten la interacción con el ciudadano.',
                  rate_torreon: 8,
                  rate_matamoros: 5,
                  rate_saltillo: 8,
                },
                {
                  title: 'Documentos de auditoría',
                  description: 'Planes, informes, cronograma y demás documentos que deriven de la realización de auditorías.',
                  rate_torreon: 8,
                  rate_matamoros: 5,
                  rate_saltillo: 8,
                },
                {
                  title: 'Información institucional',
                  description: 'Es la información relativa a la organización: misión, visión, organigrama, etc.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Documentos de gestión',
                  description: 'Se refiere a los reglamentos, la planeación estrátegica, etc.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Descarga de contenido',
                  description: 'El Sitio Web permite la descarga de contenido.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                }
              ]
            },
            {
              title: 'Disponibilidad y Calidad de la Información Relevante',
              description: 'La información relevante de la entidad hace referencia a datos y contenidos informativos sobre la identidad de la institución fiscalizadora y su funcionamiento interno.',
              score_torreon: 6.8,
              score_matamoros: 6.1,
              score_saltillo: 7.3,
              questions: [
                {
                  title: '',
                  description: ''
                },
                {
                  title: 'Reglamento interior descargable',
                  description: 'El Reglamento Interior de la Contraloría se puede descargar.',
                  rate_torreon: 10,
                  rate_matamoros: 9,
                  rate_saltillo: 10,
                },
                {
                  title: 'Organigrama de la contraloría',
                  description: 'Es posible conocer el organigrama de la organización.',
                  rate_torreon: 10,
                  rate_matamoros: 8,
                  rate_saltillo: 10,
                },
                {
                  title: 'Actividades de la contraloría',
                  description: 'Difusión de actividades de la Contraloría.',
                  rate_torreon: 8,
                  rate_matamoros: 5,
                  rate_saltillo: 8,
                },
                {
                  title: 'Contiene el cronograma de auditorías',
                  description: 'Programa anual de Auditorías.',
                  rate_torreon: 5,
                  rate_matamoros: 8,
                  rate_saltillo: 8,
                },
                {
                  title: 'Informes de las auditorías aplicadas por la contraloría',
                  description: 'Informes de las auditorías aplicadas.',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 7,
                },
                {
                  title: 'Descarga los informes de auditoría',
                  description: 'Descarga.',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 5,
                },
                {
                  title: 'Presupuesto asignado a la contraloría',
                  description: 'Presupuesto asignado.',
                  rate_torreon: 8,
                  rate_matamoros: 5,
                  rate_saltillo: 8,
                },
                {
                  title: 'Desglosa los bienes y/o servicios contratados por la contraloría',
                  description: 'Contratos vigentes',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 5,
                },
                {
                  title: 'Descarga la información de servicios',
                  description: 'Descarga',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 5,
                },
              ]
            }
          ]
        },
        participation: {
          title: 'Participación Ciudadana',
          description: 'Se refiere a la dimensión de apertura del OIC para incorporar mecanismos e instancias de cooperación y de articulación que faciliten el ejercicio de un control activo por parte de los ciudadanos y organizaciones de la sociedad civil. Es imprescindible garantizar la participación de la ciudadanía a fin de perfeccionar la calidad del control, y su involucramiento coadyuva a una mayor cultura de transparencia gubernamental.',
          entries: [
            {
              title: '',
              description: '',
              score_torreon: 0,
              score_matamoros: 0,
              score_saltillo: 0,
            },
            {
              title: 'Quejas y denuncias',
              description: 'Es el promedio ponderado del número de denuncias recibidas y las resoluciones emitidas por el Órgano Interno de Control.',
              score_torreon: 8.6,
              score_matamoros: 7.5,
              score_saltillo: 10,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Actualización quejas/denuncias en el portal del OIC',
                  description: 'Periodo en el quie se actuliza el portal de Quejas y Denuncias.',
                  rate_torreon: 9,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Unidad de Atención para quejas/denuncias',
                  description: 'El OIC cuente con un área para atención de Quejas y Denuncias.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Informe  del estado Procesal de la queja',
                  description: 'Desglose de etapas del procedimiento de quejas.',
                  rate_torreon: 9,
                  rate_matamoros: 7.5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Buzón de quejas /denuncia',
                  description: 'El OIC cuente con un buzón de quejas físico y virtual.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
              ]
            },
            {
              title: 'Perfil Contralor',
              description: 'Son las características autónomas que presenta el Contralor con respecto al gobierno Municipal.',
              score_torreon: 7.5,
              score_matamoros: 8.8,
              score_saltillo: 10,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Marco legal para designar al contralor esta homogolado con las reformas federales',
                  description: 'Requisitos y forma de designación del contralor municipal este acorde a la normatividad  federal.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Homogeneidad en la designación para ser contalor con el Codigo Municipal y Reglamento Interior',
                  description: 'Exista armonizacion de los requisitos establecidos en la legislacion estatal y municipal.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Forma de designación del OIC',
                  description: 'Procedimiento autónomo para la designación de contralores municipales.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Requisitos para el puesto de contralor y curriculum vitae están publicados en la pagina oficial',
                  description: 'Perfiles y curriculum del contralor municipal.',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
              ]
            },
            {
              title: 'Convocatoria pública al cargo de contralor',
              description: 'Son los mecanismos que utiliza el gobierno municipal para convocar a la elección de Contralor, así como el número de invitaciones de la entidad municipal con la ciudadanía.',
              score_torreon: 5,
              score_matamoros: 7,
              score_saltillo: 5,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Marco legal para emitir la convocatoria pública para designar al contralor esta homogolado con las reformas federales',
                  description: 'La convocatoria pública sea independiente imparcial y autónoma.',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 5,
                },
                {
                  title: 'Existen lineamientos para emitir y llevar a cabo la convocatoria pública al cargo de contralor ',
                  description: 'Avance de los municipios sobre lineamientos de la convocatoria pública para designar contralores municipales.',
                  rate_torreon: 5,
                  rate_matamoros: 10,
                  rate_saltillo: 5,
                },
                {
                  title: 'Plataforma digital para emitir la convocatoria pública al cargo de contralor.',
                  description: 'Avance de la plataforma digital de la convocatroria pública para designar contralores municipales.',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 5,
                },
                {
                  title: 'Intervención directa de la ciudadanía con voz y voto en',
                  description: 'En la designacion de contralores municipales que papel tiene sociedad civil.',
                  rate_torreon: 5,
                  rate_matamoros: 8,
                  rate_saltillo: 5,
                },
              ]
            },
            {
              title: 'Contraloría Social',
              description: 'Son las actividades, planes y proyectos que mantiene el Órgano de Control Interno con la sociedad civil',
              score_torreon: 10,
              score_matamoros: 8.2,
              score_saltillo: 9.5,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Participación ciudadana en la Contraloría Municipal',
                  description: 'Se refiere al grado de intervención de la ciudadanía en las Contralorias Municipales.',
                  rate_torreon: 10,
                  rate_matamoros: 8,
                  rate_saltillo: 9,
                },
                {
                  title: 'Mecanismo de participación ciudadana en la Contraloría Municipal',
                  description: 'Se refiere a la forma mediante la cual la ciudadanía participa con las Contralorias Municipales.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Normatividad para regular la participación ciudadana en la Contraloria Social',
                  description: 'Se refiere a los Reglamentos, manuales, lineamientos que le dan soporte legal a los mecanismos de participación ciudadana en las contralorias municipales.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 9,
                },
                {
                  title: 'Participación ciudadana',
                  description: 'Se refiere a la participación efectiva de la ciudadanía en las contralorias sociales, comités y comisiones',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
              ]
            },

          ]
        },
        accountability: {
          title: 'Rendición de Cuentas',
          description: 'Se refiere a los ejercicios mediante los cuales el OIC se responsabiliza de su accionar frente a la ciudadanía principal beneficiaria de la tarea de control, a través de dispositivos institucionales que permiten dar a conocer intensamente los procedimientos y actividades que desempeña. En particular, la rendición de cuentas comprende la existencia de prácticas y mecanismos a través de los cuales la entidad activamente transparente respecto de su funcionamiento interno, iniciando procedimientos de comunicación con el público y difundiendo ampliamente sus procesos y resultados.',
          entries:[
            {
              title: '',
              description: '',
              score_torreon: 0,
              score_matamoros: 0,
              score_saltillo: 0,
            },
            {
              title: 'Servidores Públicos Sancionados',
              description: 'Es el promedio ponderado de las denuncias penales interpuestas por denuncias emitidas contra servidores públicos.',
              score_torreon: 7.2,
              score_matamoros: 6.3,
              score_saltillo: 7.7,
              questions:[
                {
                  title: '',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Periodicidad del registro de servidores públicos sancionados',
                  description: 'Se refiere a la temporalidad con la que se actualiza el registro de servidores públicos sancionados.',
                  rate_torreon:9,
                  rate_matamoros: 9,
                  rate_saltillo: 9,
                },
                {
                  title: '¿Son públicas las denuncias penales, una vez concluidas derivadas de la actuación del OIC?',
                  description: 'Refiere a si el OIC hace públicas las denuncias penales de servidores públicos.',
                  rate_torreon:5,
                  rate_matamoros: 5,
                  rate_saltillo: 5,
                },
                {
                  title: 'Contenido del registro de servidores públicos sancionados',
                  description: 'Son las 4 respuestas mútliples que se refieren al estado procesal de la queja.',
                  rate_torreon:7.5,
                  rate_matamoros: 5,
                  rate_saltillo: 9,
                },
              ]
            },
            {
              title: 'Presupuesto',
              description: 'Se analiza en función del porcentaje de participación por objeto de gasto en el presupuesto total ejercido.',
              score_torreon: 9.2,
              score_matamoros: 9.2,
              score_saltillo: 9.2,
              questions:[
                {
                  title: '',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Desglose de la clasificación por objeto de gasto (concepto, presupuesto asignado y presupuesto ejercido para el 2020): Servicios personales',
                  description: 'Respuesta ante la solicitud de desglose por capítulo y concepto de presupuesto aprobado y ejercido de Servicios Personales del OIC.',
                  rate_torreon:9,
                  rate_matamoros: 9,
                  rate_saltillo: 9,
                },
                {
                  title: 'Desglose de la clasificación por objeto de gasto (concepto, presupuesto asignado y presupuesto ejercido para el 2020): Materiales y suministros',
                  description: 'Respuesta ante la solicitud de desglose por capítulo y concepto de presupuesto aprobado y ejercido de Materiales y Suministros del OIC.',
                  rate_torreon:9,
                  rate_matamoros: 9,
                  rate_saltillo: 9,
                },
                {
                  title: 'Desglose de la clasificación por objeto de gasto (concepto, presupuesto asignado y presupuesto ejercido para el 2020):: Servicios Generales',
                  description: 'Respuesta ante la solicitud de desglose por capítulo y concepto de presupuesto aprobado y ejercido de Servicios Generales del OIC.',
                  rate_torreon:9,
                  rate_matamoros: 9,
                  rate_saltillo: 9,
                },
                {
                  title: 'Desglose de la clasificación por objeto de gasto (concepto, presupuesto asignado y presupuesto ejercido para el 2020): Bienes Muebles, Inmuebles e Intangibles',
                  description: 'Respuesta ante la solicitud de desglose por capítulo y concepto de presupuesto aprobado y ejercido de Bienes Muebles, Inmuebles e Intangibles del OIC.',
                  rate_torreon:9,
                  rate_matamoros: 9,
                  rate_saltillo: 9,
                },
                {
                  title: 'Presupuesto asignado y ejercido',
                  description: 'Coincidencia entre el presupuesto total asignado y ejercido del OIC y la sumatoria del desglose por capítulo y concepto del presupuesto.',
                  rate_torreon:10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
              ]
            },
            {
              title: 'Informes de gestión',
              description: 'La elaboración de informes de gestión constituye un ejercicio integral de rendición de cuentas que realiza la entidad fiscalizadora, y se analiza en función de: 1) la disponibilidad de dichos informes para el público acceso, 2) la calidad de la información presentada, y 3) el grado de institucionalización de la práctica. Asimismo, puesto que un ejercicio activo de rendición de cuentas por parte de la entidad no comprende solamente la elaboración de informes de gestión, también se considera: 4) la existencia de instancias en las que los mismos se presentan y/o difunden ante una amplia gama de actores.',
              score_torreon: 8.5,
              score_matamoros: 7,
              score_saltillo: 8.3,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Disponibilidad de los informes',
                  description: 'Hace referencia a la posibilidad de acceso a los informes de gestión del OIC.',
                  rate_torreon: 8,
                  rate_matamoros: 8,
                  rate_saltillo: 8,
                },
                {
                  title: 'Calidad de los informes',
                  description: 'Integridad del contenido.',
                  rate_torreon: 7,
                  rate_matamoros: 9,
                  rate_saltillo: 7,
                },
                {
                  title: 'Presentación pública de los informes de gestión',
                  description: 'Existencia de la apertura del OIC en la participación de una variedad de actores como destinatarios de los informes de gestión que realiza.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Difusión de los informes de gestión',
                  description: 'Existencia de la difusión de informes de gestión.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Alcance de la presentación de los informes',
                  description: 'Alcance de la presentación de los informes',
                  rate_torreon: 7,
                  rate_matamoros: 7,
                  rate_saltillo: 7,
                },
              ]
            },
            {
              title: 'Coordinación con otros órganos fiscalizadores Estatales y/o Federales',
              description: 'Dinámicas y procesos institucionales para desarrollar actividades con otros órganos fiscalizadores.',
              score_torreon: 9,
              score_matamoros: 9,
              score_saltillo: 9,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Periodo de actualización y convenios de coordinacion con otros organos fiscalizadores estatales o federales',
                  description: 'Temporalidad para actualizar o relizar convenio con otros órganos fiscalizadores.',
                  rate_torreon:10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Firma de convenio de colaboración con otro ente para fiscalizador para el apoyo de sus funciones',
                  description: 'Existencia de convenios entre el OIC y otro ente fiscalizador.',
                  rate_torreon:10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Funciones que coordinan con otros organos fiscalizadores',
                  description: 'Actividades conuntas con otros organos fiscalizadores.',
                  rate_torreon:8,
                  rate_matamoros: 8,
                  rate_saltillo: 8,
                },
                {
                  title: 'El personal del OIC es suficiente',
                  description: 'Personal necesario para llevar a cabo las funciones necesarias de la contraloría.',
                  rate_torreon:8,
                  rate_matamoros: 8,
                  rate_saltillo: 8,
                },
              ]
            },
            {
              title: 'Padrón de proveedores y contratistas',
              description: 'Es la base de datos actualizada de los proveedores que mantienen un vínculo con el Ayuntamiento.',
              score_torreon: 9.4,
              score_matamoros: 7.8,
              score_saltillo: 9.4,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon: 0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Periodicidad de actualización de Padrón de Proveedores y Contratistas',
                  description: 'Frecuencia en la lista del Padrón de Proveedores y Contratistas.',
                  rate_torreon: 10,
                  rate_matamoros: 8,
                  rate_saltillo: 10,
                },
                {
                  title: 'Procedimiento para formar parte del padrón de proveedores y contratistas',
                  description: 'Requisitos establecidos para formar parte del Padrón de Proveedores y Contratistas.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Actividades llevadas a cabo en la revisión de expedientes.',
                  description: 'Procedimientos establecidos por parte del OIC para llevar a cabo la revisión de expedientes.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Plazo para llevar a cabo la revisión de expedientes',
                  description: 'Existencia de un plazo máximo establecido para la revisión de expedientes.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Actividades llevadas a cabo para la verificación de empresas locales',
                  description: 'Procedimientos establecidos por parte del OIC para llevar a cabo la verificación de empresas locales.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Plazo para llevar a cabo la verificación de empresas locales',
                  description: 'Existencia de un plazo máximo establecido para la verificación de empresas locales.',
                  rate_torreon: 10,
                  rate_matamoros: 8,
                  rate_saltillo: 10,
                },
                {
                  title: 'Actividades llevadas a cabo para Certificado de Aptitud',
                  description: 'Procedimientos establecidos por parte del OIC para la entrega del Certificado de Aptitud.',
                  rate_torreon: 10,
                  rate_matamoros: 9,
                  rate_saltillo:10,
                },
                {
                  title: 'Plazo para llevar la entrega del Certificado de Aptitud',
                  description: 'Existencia de un plazo máximo establecido para la entrega del Certificado de Aptitud.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Base de datos que contenga una cronología de dinámica de provedores',
                  description: 'Existencia de una base de datos que contenga la cronología del estatus de las personas físicas y morales que deseen ser parte del Padrón de Proveedores y Contratistas.',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 5,
                },
              ]
            },
            {
              title: 'Auditorías',
              description: 'Auditorías bajo las siguientes categorías: Auditorias Administrativas, Auditorias financieras, Auditorias de procedimientos administrativos y licitaciones.',
              score_torreon: 8.25,
              score_matamoros: 5,
              score_saltillo: 8.2,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Auditorías administrativas',
                  description: 'La auditoría administrativa es la evaluación y el análisis de la estructura organizaciona',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Auditorías financieras',
                  description: 'Es la evaluación de la gestión contable y económica',
                  rate_torreon: 8,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Auditorías de obras públicas',
                  description: 'Es la revisión que se efectúa entidades del sector público presupuestario para comprobar que la planeación, adjudicación, ejecución y destino de las obras públicas y demás inversiones  se hayan ajustado a la legislación y normatividad aplicable',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 7,
                },
                {
                  title: 'Auditorias de procedimientos administrativos y licitaciones',
                  description: 'Evalúa  la gestión de los procesos administrativos de licitación',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 5,
                },
              ]
            },
            {
              title: 'Solicitudes de acceso a información al OIC',
              description: 'Número de solicitudes y tipo de información solicitada al OIC.',
              score_torreon: 10,
              score_matamoros: 5,
              score_saltillo: 10,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Número de solicitudes de acceso a información sobre asuntos competentes a la Contraloría Municipal',
                  description: 'Cantidad de solicitudes realizadas.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Número de solicitudes de acceso a la información con estatus de concluído ',
                  description: 'Cantdad de solicitudes solventadas.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Número de recursos de revisión interpuestos ',
                  description: 'Cantidad de solicitudes inpugnadas.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Número de resoluciones resueltas revocando u ordenando al oic entregue la información',
                  description: 'Cantidad de resoluciones resultas por el OIC.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
              ]
            },
          ]
        },
        performance: {
          title: 'Rendimiento',
          description: 'Es el desempeño del OIC respecto a las facultades y funciones que le competen, así como la operatividad en sus procedimientos. Contempla la existencia de prácticas y mecanismos de gestión, y examina los procedimientos que permiten garantizar una labor de control imparcial.',
          entries:[
            {
              title: '',
              description: '',
              score_torreon: 0,
              score_matamoros: 0,
              score_saltillo: 0,
            },
            {
              title: 'Planificación del auditor',
              description: 'Corresponde a los sistemas organizacionales y temporales que utiliza el OIC para llevar a cabo de las auditorías.',
              score_torreon: 7.0,
              score_matamoros: 7.7,
              score_saltillo: 9.3,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Cronograma o calendarización de auditorías',
                  description: 'Consiste en la organización y sistematización de las diferentes  actividades adminitrativas realizadas por los empleados del OIC.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Manual operativo para realizar las auditorías',
                  description: 'Es el documento institucional que ampara las acciones y actividades del OIC.',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Dónde se publica la calendarización de las auditorías',
                  description: 'Consiste en la socialización de la información de la agenda del auditor.',
                  rate_torreon: 6,
                  rate_matamoros: 8,
                  rate_saltillo: 8,
                },
              ]
            },
            {
              title: 'Gestión del control',
              description: 'Consiste en el cumplimiento de la planificación, alcance de la función fiscalizadora sobre el presupuesto público local, alcance de las auditorías de gestión.',
              score_torreon: 9.6,
              score_matamoros: 5.0,
              score_saltillo: 9.2,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Plan de anual de sujetos a auditar',
                  description: 'Es la estrategia anual de sujetos a auditar.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: '% sujetos de control auditados en un año',
                  description: 'Es el cumplimiento de los sujetos auditados anualmente.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: '% del presupuesto de la administracion pública municipal auditada en un año',
                  description: 'Es la el porcentaje de auditorías que realizó en el año corriente.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Instancias de monitoreo, Area que da seguimiento',
                  description: 'Correponde a las áreas que da seguimiento y su organización.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: '% de las auditorias realizadas en un año que fueron auditorias de seguimiento de otras en las que se identificaron fallas',
                  description: 'Es la el porcentaje de auditorías que realizó en el año corriente a partir de efectuar una previa.',
                  rate_torreon: 8,
                  rate_matamoros: 5,
                  rate_saltillo: 6,
                },
              ]
            },
            {
              title: 'Calidad de gestión',
              description: 'Es la capacitación y profesionalización de los servidores públicos adscritos al OIC.',
              score_torreon: 10,
              score_matamoros: 8.8,
              score_saltillo: 10,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Cursos o capacitaciones del último año se le han impartido al personal de Órgano Inerno de Control',
                  description: 'Se refiere a la capacitacion y profesionalizacion de los servidores públicos adscritos a las contralorias municipales.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Periodicidad de capacitación de los servidores públicos adscritos al OIC',
                  description: 'Se refiere a la capacitacion y profesionalizacion de los servidores públicos adscritos a las contralorias municipales de manera continua.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Código de ética del OIC y código de conducta',
                  description: 'Normatividad del OIC para sus servidores públicos.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Perfil profesional para los servidores públicos adscritos al OIC',
                  description: 'Se refiere al perfil y curriculum de los servidores públicos adscritos a la contraloria municipal.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
              ]
            },
            {
              title: 'Política de gestión del personal',
              description: 'Procesos de contratación y verificación del conocimiento y experiencia de los servidores públicos adscritos al OIC.',
              score_torreon: 7.6,
              score_matamoros: 7,
              score_saltillo: 7.6,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Periodicidad de las convocatorias para adscribir personal al Órgano Interno de Control',
                  description: 'Se refiere a la inclusión del Servicio Profesional de Carrera dentro de las contralorias municipales.',
                  rate_torreon: 5,
                  rate_matamoros: 10,
                  rate_saltillo: 5,
                },
                {
                  title: 'Puestos y funciones del personal Adscrito al Órgano Interno de Control',
                  description: 'Organigrama de las contralorias municipales.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Tipos de contrato del personal del Órgano Interno de Control',
                  description: 'personal de confianza y sidicalizado.',
                  rate_torreon: 10,
                  rate_matamoros: 5,
                  rate_saltillo: 10,
                },
                {
                  title: 'Servicio profesional de carrera',
                  description: 'implementación del Servicio Profesional de Carrera.',
                  rate_torreon: 5,
                  rate_matamoros: 5,
                  rate_saltillo: 5,
                },
                {
                  title: 'Mecanismos formales de la evaluación de gestión',
                  description: 'Son las formas institucionales que se ejecutan para el desarrollo autocrítico de sus funciones.',
                  rate_torreon: 8,
                  rate_matamoros: 5,
                  rate_saltillo: 8,
                },
              ]
            },
            {
              title: 'Presupuesto',
              description: 'Identificar que se presente en los medios oficiales el presupuesto anual de cada Órgano de Control Interno, además observar la calidad de la información mediante el formato de presentación.',
              score_torreon: 10,
              score_matamoros: 10,
              score_saltillo: 10,
              questions:[
                {
                  title: ' ',
                  description: ' ',
                  rate_torreon:0,
                  rate_matamoros: 0,
                  rate_saltillo: 0,
                },
                {
                  title: 'Porcentaje de presupuesto ejercido en Servicios Personales con respecto al presupuesto total ejercido',
                  description: 'Proporción del presupuesto ejercido en Servicios Personales sobre el Presupuesto Total Ejercido.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Porcentaje de presupuesto ejercido en Materiales y suministros con respecto al presupuesto total ejercido',
                  description: 'Proporción del presupuesto ejercido en Materiales y Suministros sobre el Presupuesto Total Ejercido.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Porcentaje de presupuesto ejercido en Servicios Generales con respecto al presupuesto total ejercido',
                  description: 'Proporción del presupuesto ejercido en Servicios Generales sobre el Presupuesto Total Ejercido.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Porcentaje del presupuesto en Bienes muebles, Inmuebles e intangibles con respecto al presupuesto total ejercido',
                  description: 'Proporción del presupuesto ejercido en Bienes muebles, Inmuebles e Intangibles sobre el Presupuesto Total Ejercido.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
                {
                  title: 'Otro',
                  description: 'Porcentaje de auditorías realizadas a otros elementos del municipio.',
                  rate_torreon: 10,
                  rate_matamoros: 10,
                  rate_saltillo: 10,
                },
              ]
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


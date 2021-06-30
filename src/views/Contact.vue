<template lang="pug">
  section#contacto.p-5
    .container
      b-row(align-v="center" )
        b-col(md="12")
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
</template>

<script>
export default {
  name: "Contact"
}
</script>

<style scoped>

</style>

<template lang="pug">
  .social-button-container
    a.hvr-bounce-in(
      target="_blank"
      v-for="(icon, key) in icons" :key="key"
      :href="icon.href"
    )
      font-awesome-icon(
        :icon="icon.src"
        size="lg"
      ) {{ icon.title }}
</template>

<script>
export default {
  name: "FloatingSocialIcons",
  data: function () {
    return {
      icons: [
        {
          src: ['fab', 'facebook'],
          title: 'Facebook',
          href: 'https://www.facebook.com/CCILagunaAc/'
        },
        {
          src: ['fab', 'twitter'],
          title: 'Twitter',
          href: 'https://twitter.com/CCILagunaAC'
        },
        /*{
          src: ['fab', 'instagram'],
          title: 'Instagram',
          href: '#'
        },
        {
          src: ['fab', 'youtube'],
          title: 'YouTube',
          href: '#'
        }*/
      ]
    }
  },
}
</script>

<style lang="scss" scoped>
.social-button-container{
  position: fixed;
  right: 20px;
  bottom: 20px;
  a{
    margin: 10px;
  }

}
</style>

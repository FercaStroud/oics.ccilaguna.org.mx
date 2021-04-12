<template lang="pug">
  #app
    Navigator
    router-view
    FloatingSocialIcons

    .container(style="height:60px;")
</template>

<style lang="scss">

</style>
<script>
import Navigator from "@/components/Navigator";
import FloatingSocialIcons from "@/components/FloatingSocialIcons";

export default {
  components: {FloatingSocialIcons, Navigator}
}
</script>
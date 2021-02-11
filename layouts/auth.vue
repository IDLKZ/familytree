<template>
  <v-app>
    <Nuxt/>
  </v-app>
</template>

<script>
  export default {
    middleware: 'guest',
    name: "auth"
  }
</script>

<style scoped>

</style>

<template>

  <v-app style="overflow: hidden!important;">
    <Header></Header>
    <v-main>
      <Nuxt/>
    </v-main>
    <Footer></Footer>
  </v-app>





</template>

<script>
import Header from "../components/Header";
import Footer from "../components/Footer";
export default {
name: "layout.vue",
  components: {Footer, Header}
}
</script>

<style scoped>

</style>

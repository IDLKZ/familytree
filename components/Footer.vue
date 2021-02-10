<template>
  <v-footer
    dark
    padless
    color="green darken-2"
  >
    <v-row
      justify="center"
      no-gutters
    >
        <v-col cols="12" class="text-center py-2">
          <v-btn
            v-for="icon in icons"
            :key="icon"
            class="mx-4 white--text"
            icon
          >
            <v-icon size="24px">
              {{ icon }}
            </v-icon>
          </v-btn>
        </v-col>


      <v-btn
        v-for="link in links"
        :key="link"
        color="white"
        text
        rounded
        class="my-2"
        link
        :to="link.url"
      >
        {{ link.title }}
      </v-btn>
      <v-col
        class="dark py-4 text-center white--text"
        cols="12"
      >
        {{ new Date().getFullYear() }} — <strong>Tree Family</strong>
      </v-col>
    </v-row>
  </v-footer>
</template>

<script>
export default {
name: "Footer",
  data: () => ({
    links:[
      {title:"Главная",url:"/"},
      {title:"О нас",url:"/about"},
      {title:"Шежіре",url:"/shejire"},
      {title:"Галерея",url:"/gallery"},
      {title:"Новости",url:"/news"},
      {title:"Контакты",url:"/contact"},
    ],
    icons: [
      'mdi-facebook',
      'mdi-twitter',
      'mdi-linkedin',
      'mdi-instagram',
    ],
  }),

}
</script>

<style scoped>

</style>

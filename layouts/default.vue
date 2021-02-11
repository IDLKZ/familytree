<template>
  <v-app dark>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-bottom-navigation v-model="value" dark>
      <v-btn value="recent" link to="/profile">
        <span>Главная</span>

        <v-icon>mdi-view-dashboard</v-icon>
      </v-btn>

      <v-btn value="recent" link to="/profile/user/create">
        <span>Добавить пользователя</span>

        <v-icon>mdi-account-multiple-plus</v-icon>
      </v-btn>

      <v-btn value="favorites" link to="/profile/gallery">
        <span>Галерея</span>
        <v-icon>mdi-camera</v-icon>
      </v-btn>
      <v-btn value="favorites" link to="/profile/news">
        <span>Новостной блог</span>
        <v-icon>mdi-newspaper</v-icon>
      </v-btn>

      <v-btn value="nearby" @click="logout">
        <span>Выход</span>

        <v-icon>mdi-logout-variant</v-icon>
      </v-btn>
    </v-bottom-navigation>
  </v-app>
</template>

<script>
export default {
  middleware: 'auth',
  data () {
    return {
      value: 'recent'
    }
  },
  methods: {
    logout() {
      this.$auth.logout()
    }
  }
}
</script>

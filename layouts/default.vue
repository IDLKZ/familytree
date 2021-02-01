<template>
  <v-app dark>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-bottom-navigation v-model="value">
      <v-btn value="recent" link to="/profile">
        <span>Главная</span>

        <v-icon>mdi-view-dashboard</v-icon>
      </v-btn>

      <v-btn value="recent" link to="/profile/user/create">
        <span>Добавить пользователя</span>

        <v-icon>mdi-account-multiple-plus</v-icon>
      </v-btn>

      <v-btn value="favorites">
        <span>Favorites</span>

        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <v-btn value="nearby">
        <span>Выход</span>

        <v-icon>mdi-logout-variant</v-icon>
      </v-btn>
    </v-bottom-navigation>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      value: 'recent'
    }
  }
}
</script>

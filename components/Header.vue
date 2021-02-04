<template>
  <div>
  <v-navigation-drawer
  temporary v-model="drawer" absolute>


  </v-navigation-drawer>

  <v-app-bar app elevation="0" dark>
    <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

    <v-toolbar-title>Title</v-toolbar-title>
  </v-app-bar>
  </div>
</template>

<script>
export default {
  name: "Header",
  data(){
    return{
      drawer:false
    }
  }
}
</script>

<style scoped>

</style>

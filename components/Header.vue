<template>
  <div class="transparent">
  <v-navigation-drawer
  temporary v-model="drawer" absolute>


  </v-navigation-drawer>

  <v-app-bar app elevation="0" color="green darken-2" dark>
    <v-app-bar-nav-icon @click="drawer = !drawer" class="d-sm-none d-block"></v-app-bar-nav-icon>
    <v-toolbar-title style="overflow: visible!important">Family Tree</v-toolbar-title>
    <v-tabs style="display: flex!important; justify-content: center!important; padding-right: 24px">
      <v-tab v-for="(item,i) in links" :key="i" link :to="item.url" class="ml-5">
        {{item.title}}
      </v-tab>
    </v-tabs>
    <v-btn class="rounded transparent border-white-fade-50">
      Оставить заявку
    </v-btn>
  </v-app-bar>
  </div>
</template>

<script>
export default {
  name: "Header",
  data(){
    return{
      drawer:false,
     collapseOnScroll:false,
      links:[
        {title:"Главная",url:"/"},
        {title:"О нас",url:"/"},
        {title:"Шежіре",url:"/shejire"},
        {title:"Галерея",url:"/"},
        {title:"Новости",url:"/"},
        {title:"Контакты",url:"/"},
      ]
    }
  },
  mounted() {

  },
  methods:{

  }
}
</script>

<style scoped>

</style>

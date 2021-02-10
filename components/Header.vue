<template>
  <div class="transparent">
  <v-navigation-drawer
  temporary v-model="drawer" absolute>


  </v-navigation-drawer>

  <v-app-bar app elevation="0" color="green darken-2" dark>
    <v-toolbar-title style="overflow: visible!important; padding-left: 20px">Family Tree</v-toolbar-title>
      <v-tabs class="top-navbar" style="justify-content: center!important; padding-right: 24px">
        <v-tab v-for="(item,i) in links" :key="i" link :to="item.url" class="ml-5">
          {{item.title}}
        </v-tab>
      </v-tabs>

    <v-btn
      rounded
      dark
      outlined
      link
      class=" border-white-fade-50 top-button">
      <v-icon class="pr-2">mdi-email</v-icon>
      Оставить заявку
    </v-btn>
    <v-btn
      rounded
      dark
      outlined
      @click="drawer = !drawer"
      class="drawer-button"
      >
      <v-icon> mdi-format-list-bulleted-square </v-icon>
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
        {title:"О нас",url:"/about"},
        {title:"Шежіре",url:"/shejire"},
        {title:"Галерея",url:"/gallery"},
        {title:"Новости",url:"/news"},
        {title:"Контакты",url:"/contact"},
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
@media screen and (max-width: 900px){
  .top-navbar{
    display: none!important;
  }
  .top-button{
    display: none;
  }
  .drawer-button{
    display: none;
  }
}
@media screen and (min-width: 900px){
  .top-navbar{
    display: flex!important;
  }
  .top-button{
    display: block;
  }
  .drawer-button{
    display: block;
  }
}
</style>

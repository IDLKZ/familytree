<template>
  <div class="transparent">
  <v-navigation-drawer
  temporary v-model="drawer" absolute>
    <v-card height="350px">
      <v-navigation-drawer
        absolute
        permanent
        right
      >
        <template v-slot:prepend>
          <v-list-item two-line>
            <v-list-item-avatar>
              <img src="/logo.png">
            </v-list-item-avatar>

            <v-list-item-content>
              <v-list-item-title>ШЕЖІРЕ</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </template>

        <v-divider></v-divider>

        <v-list>
          <v-list-item
            v-for="item in links"
            :key="item.title"
            :to="item.url"
            link
          >
            <v-list-item-icon>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-navigation-drawer>
    </v-card>

  </v-navigation-drawer>

  <v-app-bar app elevation="0" color="green darken-2" dark>

    <v-toolbar-title to="/" link class="cursor-pointer" style="overflow: visible!important; padding-left: 10px">
      <v-img src="/logo.png" height="55" width="55"></v-img>

      </v-toolbar-title>
    <b class="pl-1">
      ШЕЖІРЕ
    </b>

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
    <v-spacer></v-spacer>
      <v-btn
        right
        dark
        outlined
        @click="drawer = !drawer"
        class="drawer-button"
      >
        <v-icon>mdi-view-headline</v-icon>
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
        {title:"Главная",url:"/",icon:"mdi-home"},
        {title:"О нас",url:"/about",icon:"mdi-home-heart"},
        {title:"Шежіре",url:"/shejire",icon:"mdi-account-multiple-outline"},
        {title:"Галерея",url:"/gallery",icon:"mdi-camera"},
        {title:"Новости",url:"/news",icon:"mdi-newspaper"},
        {title:"Контакты",url:"/contact",icon:"mdi-account"},
      ],
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
    display: block;
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
    display: none;
  }
}
</style>

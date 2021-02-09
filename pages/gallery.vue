<template>

  <div>
    <v-container fluid>
    <v-row>
      <v-col cols="12" style="padding: 0!important;">
        <v-parallax height="200" class="pa-0"
                    gradient="to top right, rgba(100,115,201,.33), rgba(25,32,72,.7)"
                    src="/breadcrumbs1.png"
        >
          <v-breadcrumbs
            :items="items"
            divider="/"
            large
          ></v-breadcrumbs>

        </v-parallax>
      </v-col>
    </v-row>
  </v-container>
    <v-container class="my-5 py-5" v-if="images.length">
      <v-row>
        <v-col cols="12" md="4" v-for="(image, i) in images" :key="i">
          <v-card
            class="mx-auto"
            max-width="350"
            min-height="320"
            @click="onClick(i)"
          >
            <v-img
              :src="image.url"
              height="200px"
            ></v-img>

            <v-card-title>
              {{image.alt}}
            </v-card-title>


          </v-card>
        </v-col>
      </v-row>
      <vue-gallery-slideshow :images="images" :index="index" @close="index = null"></vue-gallery-slideshow>
      <v-col cols="12" class="text-center" v-if="currentPage<lastPage">
        <v-btn class="primary" @click="loadData">Загрузить еще...</v-btn>
      </v-col>
    </v-container>
  </div>

</template>

<script>
import VueGallerySlideshow from 'vue-gallery-slideshow'
export default {
  name: "index",
  layout:"layout",
  components:{
    VueGallerySlideshow
  },
  data(){
    return{
      images: [],
      index: 0,
      currentPage:1,
      lastPage:1,
      items: [
        {
          text: 'Главная',
          disabled: false,
          to: '/',
        },
        {
          text: 'Галерея',
          disabled: false,
          href: '/gallery',
          to: '/gallery',
        },

      ],
    }
  },


  methods: {
    onClick(i) {
      this.index = i;
    },
    async initiateData(){
      let self = this;
      await this.$axios.$get("gallery").then(function (response)
      {
        self.images = [];
        self.currentPage = 1;
        self.lastPage = response["last_page"];
        for(let i = 0; i<response.data.length; i++){
          self.images[i] = {url:self.$store.state.image.image + response.data[i].img, alt:response.data[i].title,id:response.data[i].id};
        }
      });


    },
    async loadData(){
      let self = this;
      await this.$axios.$get("gallery?page="+ (+this.currentPage + 1)).then(function (response)
      {
        self.currentPage = response["current_page"];
        self.lastPage = response["last_page"];
        console.log(response);
        for(let i = 0; i<response.data.length; i++){
          self.images.push({url:self.$store.state.image.image + response.data[i].img, alt:response.data[i].title,id:response.data[i].id});
        }
      });
    },

  },
  async asyncData({$axios,store}){
    let images = [];
    let currentPage;
    let lastPage;
    await $axios.$get("gallery").then(function (response)
      {
        currentPage = response["current_page"];
        lastPage = response["last_page"];
        for(let i = 0; i<response.data.length; i++){
          images[i] = {url:store.state.image.image + response.data[i].img, alt:response.data[i].title, id:response.data[i].id};
        }
      }
    );
    return {images,currentPage,lastPage};
  }

}
</script>

<style scoped>

</style>

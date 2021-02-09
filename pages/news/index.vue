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
    <v-container class="my-5 py-5" v-if="news.length">
      <v-row>
        <v-col cols="12" md="4" v-for="(image, i) in news" :key="i">
          <v-card
            class="mx-auto"
            max-width="350"
            min-height="320"
          >
            <v-img
              :src="$store.state.image.image + image.img"
              height="200px"
            ></v-img>

            <v-card-title>
              {{image.title}}
            </v-card-title>
            <v-spacer></v-spacer>
            <v-card-subtitle>
              {{image.content}}
            </v-card-subtitle>
            <v-card-actions>
              <v-btn class="primary" :to="'/news/'+image.id">
                Читать
              </v-btn>
            </v-card-actions>

          </v-card>
        </v-col>
      </v-row>
      <v-col cols="12" class="text-center" v-if="currentPage<lastPage">
        <v-btn class="primary" @click="loadData">Загрузить еще...</v-btn>
      </v-col>
    </v-container>



  </div>
</template>

<script>
export default {
  name: "index",
  layout:"layout",
  data(){
    return{
      news: [],
      currentPage:1,
      lastPage:1,
      items: [
        {
          text: 'Главная',
          disabled: false,
          to: '/',
        },
        {
          text: 'Новости',
          disabled: false,
          href: '/gallery',
          to: '/news',
        },

      ],
    }
  },


  methods: {
    onClick(i) {
      this.index = i;
    },
    uploadImg(e){
      this.form.img = e;
    },
    uploadUpdateImg(e){
      this.currentForm.img = e;
    },

    async loadData(){
      let self = this;
      await this.$axios.$get("news?page="+ (+this.currentPage + 1)).then(function (response)
      {
        self.currentPage = response["current_page"];
        self.lastPage = response["last_page"];
        console.log(response);
        for(let i = 0; i<response.data.length; i++){
          self.news.push(response.data[i]);
        }
      });
    },
    async removeData(id){
      await this.$axios.$delete("/news-delete/"+ id);
      await this.initiateData();
    }
  },
  async asyncData({$axios,store}){
    let news = [];
    let currentPage;
    let lastPage;
    await $axios.$get("news").then(function (response)
      {
        currentPage = response["current_page"];
        lastPage = response["last_page"];
        news = response.data;
      }
    );
    return {news,currentPage,lastPage};
  }

}
</script>

<style scoped>

</style>

<template>
  <div>
    <v-container>
      <v-row v-if="news">
        <v-col cols="12" md="12">
          <v-img max-height="450" :src="$store.state.image.image  + news.img"></v-img>
        </v-col>
        <v-col cols="12">
          <div class="text-h4">
            {{news.title}}
          </div>
          <div class="text-subheading">
            {{news.content}}
          </div>
        </v-col>
      </v-row>



    </v-container>


  </div>
</template>

<script>
export default {
  name: "_alias",
  layout:"layout",
  data(){
    return{
      news:[]
    }
  },
  mounted() {

  },
  async asyncData({$axios,params}){
    let news = await $axios.$get("/news-show/"+params.alias);
    return {news}
  }
}
</script>

<style scoped>

</style>

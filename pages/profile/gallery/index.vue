<template>
<div>
  <v-fab-transition>
    <v-btn
      color="green"
      style="position: fixed; z-index: 2; bottom:20px; right: 20px"
      fab
      large
      dark
      class=" v-btn--example"
      @click="dialog2 = !dialog2"
    >
      <v-icon>mdi-plus</v-icon>
    </v-btn>
  </v-fab-transition>
  <v-container v-if="images.length">
    <v-row>
      <v-col cols="12" md="4" v-for="(image, i) in images" :key="i">
        <v-card
          class="mx-auto"
          max-width="350"
          min-height="320"
        >
          <v-img
            :src="image.url"
            height="200px"
          ></v-img>

          <v-card-title>
            {{image.alt}}
          </v-card-title>

          <v-card-actions class="">
            <v-btn
              outlined
            color="green lighten-2"
            text
            @click="onClick(i)"
          >
            <v-icon>mdi-eye</v-icon>
          </v-btn>
            <v-btn
              outlined
              color="blue lighten-2"
              text
              @click="update(image)"
            >
              <v-icon>mdi-pencil</v-icon>
            </v-btn>
            <v-btn
              outlined
              color="red lighten-2"
              text
              @click="removeData(image.id)"
            >
              <v-icon>mdi-bucket</v-icon>
            </v-btn>

            <v-spacer></v-spacer>

          </v-card-actions>

        </v-card>
      </v-col>
    </v-row>
    <vue-gallery-slideshow :images="images" :index="index" @close="index = null"></vue-gallery-slideshow>
    <v-col cols="12" class="text-center" v-if="currentPage<lastPage">
      <v-btn class="primary" @click="loadData">Загрузить еще...</v-btn>
    </v-col>
  </v-container>
<!--  Dialog window-->
  <v-dialog
    v-model="dialog2"
    dark
    max-width="500px"
  >
    <v-card>
      <v-card-title>
        Добавить новое изображение галереи
      </v-card-title>
      <v-divider></v-divider>
      <v-card-subtitle>
        <v-form @submit.prevent="saveData">
          <v-file-input
            show-size
            truncate-length="15"
            label="Изображение"
            accept="image/*"
            required
            @change="uploadImg"
            ref="img"
          ></v-file-input>
          <v-text-field
            required
          label="Описание изображения"
            v-model="form.title"
          ></v-text-field>

            <v-btn
              color="primary"
              class="mr-4"
              type="submit"
            >
              Сохранить
            </v-btn>
            <v-btn
              color="primary"
              text
              @click="dialog2 = false"
            >
              Отмена
            </v-btn>


        </v-form>
      </v-card-subtitle>


    </v-card>

  </v-dialog>
<!--Dialog update window-->
  <v-dialog
    v-model="dialog3"
    dark
    max-width="500px"
  >
    <v-card>
      <v-card-title>
        Изменить изображение галереи
      </v-card-title>
      <v-divider></v-divider>
      <v-card-subtitle>
        <v-img
          :src="image"
          height="200px"
        ></v-img>
        <v-form @submit.prevent="updateData">
          <v-file-input
            show-size
            truncate-length="15"
            label="Изображение"
            accept="image/*"
            required
            @change="uploadUpdateImg"
            ref="currentImg"
          ></v-file-input>
          <v-text-field
            required
            label="Описание изображения"
            v-model="currentForm.title"
          >
          </v-text-field>

          <v-btn
            color="primary"
            class="mr-4"
            type="submit"
          >
            Изменить
          </v-btn>
          <v-btn
            color="primary"
            text
            @click="dialog3 = false"
          >
            Отмена
          </v-btn>


        </v-form>
      </v-card-subtitle>


    </v-card>

  </v-dialog>


</div>
</template>

<script>
import VueGallerySlideshow from 'vue-gallery-slideshow'
export default {
name: "index",
  components:{
    VueGallerySlideshow
  },
  data(){
  return{
    form:{
      img:"",
      title:""
    },
    currentForm:{
      img:"",
      title:"",
    },
    image:"",
    images: [],
    index: 0,
    dialog2:false,
    dialog3:false,
    currentPage:1,
    lastPage:1,
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
    async saveData(){
      if(this.form.img){
        const formData = new FormData();
        Object.keys(this.form).forEach((key) => {
          if(this.form[key] != null){
            formData.append(key, this.form[key])
          }
        })
        let config = {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        };
        await this.$axios.$post('gallery-create', formData,config).then(async (e) => {
          this.$toast.success('Публикация успешно создана');
          this.resetData();
          this.initiateData();

        }).catch(error => {
          this.errors = error.response.data
        })
      }
      else{
        this.$toast.error("Добавьте изображения!");
      }

    },
    async updateData(){
        const formData = new FormData();
        Object.keys(this.currentForm).forEach((key) => {
          if(this.currentForm[key] != null){
            formData.append(key, this.currentForm[key])
          }
        })
        let config = {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        };
        await this.$axios.$post('gallery-update', formData,config).then(async (e) => {
          console.log(e);
          this.$toast.success('Публикация успешно создана');
          this.initiateData();
          this.currentForm.img = "";
          this.currentForm.title = "";
          this.$refs.currentImg.reset();
          this.dialog3 = false;

        }).catch(error => {
          this.errors = error.response.data
        })


    },
    resetData(){
      this.form.img = "";
      this.form.title = "";
      this.$refs.img.reset();
    },
    update(item){
      this.image = item.url;
      this.currentForm.title = item.alt;
      this.currentForm.id = item.id;
      this.dialog3 = true;
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
    async removeData(id){
      await this.$axios.$delete("/gallery-delete/"+ id);
      await this.initiateData();
    }
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

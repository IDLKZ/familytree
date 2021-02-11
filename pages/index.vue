<template>
  <div>
    <section>
      <v-container fluid class="m-0 p-0">

        <v-row>

          <v-col cols="12" class="custom-parallax">
            <v-parallax src="bg.png" class="bg-image" height="100vh">
              <v-row
                align="center"
                justify="center"
              >
                <v-col
                  class="text-center"
                  cols="12"
                >
                    <h1 class=" mb-4 bg-title">
                      Найди своего предка!
                    </h1>

                  <h3 class="subheading bounce" >
                   Поможем Вам найти Ваших Родственников!
                  </h3>

                </v-col>
              </v-row>
            </v-parallax>
          </v-col>
        </v-row>
      </v-container>
    </section>
    <section class="my-5 py-5">
      <v-container>
        <v-row>
          <v-col cols="12" md="12" class="text-center my-5">
            <h1 class="text-h3 text-bold mb-2">О чем этот сайт</h1>
            <p class="text-h5 text-bold">Чем мы занимаемся</p>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="4" v-for="(item,index) in targets" :key="index">
            <v-card
              class="mx-auto text-center"
              min-height="300"
              max-width="400"
            >
              <v-img
                class="image-circle"
                height="200px"
                :src="item.img"
              >
              </v-img>
              <div class="text-center">
                <v-card-subtitle class="pb-0 justify-center text-h6">
                  {{item.title}}
                </v-card-subtitle>
              </div>


            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </section>
    <hr>
    <section class="my-5 py-5">
      <v-container>
        <v-row>
          <v-col cols="12" md="12" class="text-center my-5">
            <h1 class="text-h3 text-bold mb-2">Немного о нас</h1>
            <p class="text-h5 text-bold">Пару слов о Нас</p>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="6">
            <lottie :options="lottieOptions.social" v-on:animCreated="handleAnimation" />
          </v-col>
          <v-col cols="12" md="6">
            <v-card
            color="light-green lighten-1"
            >
              <v-toolbar
                dark
                flat
                color="green darken-2"
              >
                  <v-app-bar-title>Немного о Нас</v-app-bar-title>
                <template v-slot:extension>
                  <v-tabs
                    v-model="tab"
                    align-with-title
                    next-icon="mdi-arrow-right-bold-box-outline"
                    prev-icon="mdi-arrow-left-bold-box-outline"
                  >
                    <v-tabs-slider color="yellow"></v-tabs-slider>

                    <v-tab
                      v-for="item in items"
                      :key="item"
                    >
                      {{ item.title }}
                    </v-tab>
                  </v-tabs>
                </template>
              </v-toolbar>

              <v-tabs-items v-model="tab">
                <v-tab-item
                  v-for="item in items"
                  :key="item"
                >
                  <v-card flat>
                    <v-card-text v-text="item.text"></v-card-text>
                  </v-card>
                </v-tab-item>
              </v-tabs-items>
            </v-card>


          </v-col>
        </v-row>
      </v-container>
    </section>
    <hr>
    <section class="my-5 py-5">
      <v-container>
        <v-row>
          <v-col cols="12" md="12" class="text-center my-5">
            <h1 class="text-h3 text-bold mb-2">Известные члены семьи</h1>
            <p class="text-h5 text-bold">Члены семьи</p>
          </v-col>
        </v-row>
        <v-row>
          <carousel-3d>
            <slide v-for="(slide, i) in members" :index="i" style="background-color: white" :key="i">
              <v-col class="px-2">
                <v-card
                  class="mx-auto text-center"
                  min-height="300"
                  elevation="0"
                >
                  <v-img
                    class="image-circle"
                    height="200px"
                    :src="$store.state.image.image + slide.img"
                  >
                  </v-img>
                  <div class="text-center">
                    <v-card-subtitle class="pb-0 justify-center text-h6">
                      {{slide.name}}
                    </v-card-subtitle>
                  </div>
                </v-card>

              </v-col>
            </slide>
          </carousel-3d>
        </v-row>
      </v-container>
    </section>
    <hr>
    <section class="my-5 py-5">
      <v-container>
        <v-row>
          <v-col cols="12" md="12" class="text-center my-5">
            <h1 class="text-h3 text-bold mb-2">Новости</h1>
            <p class="text-h5 text-bold">Последние новости</p>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" class="text-center my-2">
          <VueSlickCarousel class="my-sm-2" :arrows="true" :dots="true" v-bind="settings">
            <div  class="pa-md-10 pa-sm-5" v-for="(item,index) in news" :key="index">
              <v-card
                class="mx-auto"
                max-width="400"
                min-height="450"
              >
                <v-img
                  class="white--text"
                  height="200px"
                  :src="$store.state.image.image + item.img"
                >

                </v-img>
                <v-card-title class="my-5">{{item.title}}</v-card-title>
                <v-card-subtitle class="pb-0 text-left mt-2 mb-2">
                  {{new Date(item.created_at).toString("dd-mm-yyyy")}}
                </v-card-subtitle>

                <v-card-text class="text--primary text-left">
                  <div>
                    {{item.content.length > 120 ? item.content.substr(0,120) + '....' : item.content}}
                  </div>
                </v-card-text>

                <v-card-actions>
                  <v-btn
                    color="gray"
                    text
                    :to = "'/news/' + item.id"
                  >
                    Читать <v-icon>mdi-chevron-right</v-icon>
                  </v-btn>

                </v-card-actions>
              </v-card>
            </div>
          </VueSlickCarousel>
          </v-col>
        </v-row>
      </v-container>
    </section>
    <hr>
    <section class="my-5 py-5">
      <v-container>
        <v-row>
          <v-col cols="12" md="12" class="text-center my-5">
            <h1 class="text-h3 text-bold mb-2">Как добавить родственника?</h1>
            <p class="text-h5 text-bold">F.A.Q</p>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="12">
            <v-stepper
              v-model="e6"
              vertical
            >
              <v-stepper-step
                :complete="e6 > 1"
                step="1"
                editable
              >
               Перейдите в Контакты
              </v-stepper-step>

              <v-stepper-content step="1">
                <v-card
                  color=""
                  class="mb-12"
                  height="200px"
                ></v-card>
                <v-btn
                  color="primary"
                  @click="e6 = 2"
                >
                  Продолжить
                </v-btn>
              </v-stepper-content>

              <v-stepper-step
                :complete="e6 > 2"
                step="2"
                editable
              >
                Написать нам
              </v-stepper-step>

              <v-stepper-content step="2">
                <v-card
                  color="grey lighten-1"
                  class="mb-12"
                  height="200px"
                ></v-card>
                <v-btn
                  color="primary"
                  @click="e6 = 3"
                >
                  Продолжить
                </v-btn>
              </v-stepper-content>

              <v-stepper-step
                :complete="e6 > 3"
                step="3"
                editable
              >
                Выберите тип контактов
              </v-stepper-step>

              <v-stepper-content step="3">
                <v-card
                  color="grey lighten-1"
                  class="mb-12"
                  height="200px"
                ></v-card>
                <v-btn
                  color="primary"
                  @click="e6 = 4"
                >
                  Продолжить
                </v-btn>
              </v-stepper-content>

              <v-stepper-step step="4" editable>
                Что отправить?
              </v-stepper-step>
              <v-stepper-content step="4">
                <v-card
                  color="grey lighten-1"
                  class="mb-12"
                  height="200px"
                ></v-card>

              </v-stepper-content>
            </v-stepper>

          </v-col>

        </v-row>
      </v-container>
    </section>

  </div>

</template>

<script>
import VueSlickCarousel from 'vue-slick-carousel';
import 'vue-slick-carousel/dist/vue-slick-carousel.css';
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css';
import { Carousel3d, Slide } from 'vue-carousel-3d';
import lottie from 'vue-lottie/src/lottie.vue';
import * as social from "static/animation/social.json";
export default {
  layout:"layout",
  components:{
    VueSlickCarousel,Carousel3d,Slide,lottie
  },
  data(){
    return{
      e6: 1,
      items: [
        {title:"Кто мы",text:"1Lorem ipsum dolor sit amet, consectetur adipiscing elit, sedLorem ipsum dolor sit amet, consectetur adipiscing elit, sedLorem ipsum dolor sit amet, consectetur adipiscing elit, sedLorem ipsum dolor sit amet, consectetur adipiscing elit, sed"},
        {title:"Какова Наша Цель",text:"2Lorem ipsum dolor sit amet, consectetur adipiscing elit, sedLorem ipsum dolor sit amet, consectetur adipiscing elit, sedLorem ipsum dolor sit amet, consectetur adipiscing elit, sedLorem ipsum dolor sit amet, consectetur adipiscing elit, sed"},
        {title:"Что такое Шежире",text:"3Lorem ipsum dolor sit amet, consectetur adipiscing elit, sedLorem ipsum dolor sit amet, consectetur adipiscing elit, sedLorem ipsum dolor sit amet, consectetur adipiscing elit, sedLorem ipsum dolor sit amet, consectetur adipiscing elit, sed"},
      ],
      tab:null,
      lottieOptions: {
        social: { animationData: social.default },
      },
      settings:{
        "dots": true,
        "infinite": false,
        "speed": 500,
        "slidesToShow": 3,
        "slidesToScroll": 1,
        "initialSlide": 0,
        "responsive": [

          {
            "breakpoint": 1024,
            "settings": {
              "slidesToShow": 3,
              "slidesToScroll": 3,
              "infinite": true,
              "dots": true
            }
          },

          {
            "breakpoint": 900,
            "settings": {
              "slidesToShow": 2,
              "slidesToScroll": 2,
              "initialSlide": 2,
              "dots": true
            }
          },
          {
            "breakpoint": 480,
            "settings": {
              "slidesToShow": 1,
              "slidesToScroll": 1,
              "dots": true

            }
          }
        ]
      }
    }
  },
  methods: {
    handleAnimation: function (anim) {
      this.anim = anim;
    }
  },
  computed:{
    targets(){
      return[
        {img:"1.png",title:"Храним семейные ценности"},
        {img:"2.png",title:"Генеалогическое дерево Вашей семьи"},
        {img:"3.png",title:"Оставайся на связи с родными!"},
      ]
    }
  },
  async asyncData({$axios}){
    let members = await $axios.$get("/member");
    let news = await $axios.$get("/data");
    return {members,news}
  }

}
</script>
<style>
.custom-parallax{
  height: 100%!important;
  width: 100%;
  padding: 0!important;
}
.bg-image{
  height: 100vh!important;
  background-size: cover!important;
  background-position: center center!important;
}
.bg-title{
  font-size: 42px!important;
}
.image-circle{
  height: 200px!important;
  width: 200px!important;
  border-radius: 50%!important;
  justify-content: center;
  display: inline-block!important;
}



</style>

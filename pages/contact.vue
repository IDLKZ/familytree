<template>
<div>
  <!-- width and height are optional -->
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
  <v-container>
    <v-row>
      <v-col cols="12" md="6">

      </v-col>
      <v-col cols="12" md="6">
        <lottie :width="'100%'" :height="450" :options="lottieOptions" v-on:animCreated="handleAnimation" />

      </v-col>
    </v-row>
  </v-container>


</div>
</template>

<script>
import lottie from 'vue-lottie/src/lottie.vue';
import * as animationData from "static/animation/contact.json";
export default {
name: "contact",
  layout:"layout",
  components: {
    lottie
  },
  data() {
    return {
      anim: null, // for saving the reference to the animation
      lottieOptions: { animationData: animationData.default },
      items: [
        {
          text: 'Главная',
          disabled: false,
          to: '/',
        },
        {
          text: 'Контакты',
          disabled: false,
          href: '/contact',
          to: '/contact',
        },

      ],
    };
  },
  methods: {
    handleAnimation: function (anim) {
      this.anim = anim;
    }
  }
}
</script>

<style scoped>

</style>

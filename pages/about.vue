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
  <v-container fluid>
    <v-row class="my-5 py-5">
      <v-col cols="12" md="6" >
        <v-img src="/aboutus.png">
          <div class="fill-height bottom-gradient"></div>
        </v-img>
      </v-col>
      <v-col cols="12" md="6">
        <div class="text-h4 mb-5">Немного о нас</div>
        <div class="text-subheading">
          Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
        </div>
      </v-col>
    </v-row>
  </v-container>
</div>
</template>

<script>
export default {
name: "about",
  layout:"layout",
  data: () => ({
    items: [
      {
        text: 'Главная',
        disabled: false,
        to: '/',
      },
      {
        text: 'О нас',
        disabled: false,
        href: '/about',
        to: '/about',
      },

    ],
  }),
}
</script>

<style scoped>

</style>

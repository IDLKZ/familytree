<template>
  <v-container>
    <h2>Редактировать пользователя</h2>
    <v-form
      ref="form"
      v-on:submit.prevent="update($route.params.id)"
    >
      <v-text-field
        v-model="form.name"
        :counter="10"
        label="Имя"
        required
      ></v-text-field>

      <v-autocomplete
        ref="ancestor"
        v-if="!ancestor"
        auto-select-first
        clearable
        dense
        v-model="form.parent_id"
        :items="items"
        item-text="name"
        item-value="id"
        label="Выберите родителя"
        @change="parent"
      ></v-autocomplete>
      <v-text-field
        v-model="form.number"
        label="Сын"
        required
      ></v-text-field>
      <v-img
        max-height="150"
        max-width="250"
        :src="getImages(form.img)"
      ></v-img>
      <v-file-input
        counter
        show-size
        truncate-length="15"
        accept="image/*"
        @change="uploadImg"
        label="Выберите картинку (необязательно)"
      ></v-file-input>
      <label>Описание (необязательно)</label>
      <ckeditor-nuxt v-model="form.description" :config="editorConfig"></ckeditor-nuxt>
      <br>
      <v-btn
        color="success"
        type="submit"
      >
        Обновить
      </v-btn>
    </v-form>
  </v-container>
</template>

<script>
    export default {
      components: {
        'ckeditor-nuxt': () => { if (process.client) { return import('@blowstack/ckeditor-nuxt') } },
      },
      data() {
        return {
          description: '',
          editorConfig: {
            removePlugins: ['Title'],
          },
          items: [],
          form: {
            name: '',
            parent_id: '',
            img: '',
            description: '',
            number:1
          },
          ancestor:false,
        }
      },
      methods: {
        async update(id) {
          try {
            const formData = new FormData();
            Object.keys(this.form).forEach((key) => {
              if(this.form[key] != null){
                formData.append(key, this.form[key])
              }
            })
            if (this.form.img == '') {
              formData.delete('img')
            }
            let config = {
              headers: {
                'Content-Type': 'multipart/form-data'
              }
            };
            formData.append("_method","PATCH");
            await this.$axios.$post('/families/'+id, formData,config).then(async (e) => {
              this.$toast.success('Публикация успешно обновлена')
              this.$nuxt.$router.replace({ path: '/profile/list'})
            }).catch(error => {
              this.errors = error.response.data
            })

          }
          catch (e) {
            console.log(e)
          }
        },
        loadCategories() {
          this.$axios.get('/families/'+this.$route.params.id).then(({data}) => (
            [
              // console.log(data.data)
              this.form.name = data.name,
              this.form.parent_id = data.parent_id,
              this.form.img = data.img,
              // this.form.description = data.description,
              this.form.number = data.number,
              data.parent_id == null ? this.ancestor = true : this.ancestor = false
            ]
          ))
        },
        loadDescription(){
          this.$axios.get('/families/'+this.$route.params.id).then(({data}) => (
            [
              this.form.description = data.description,
            ]
          ))
        },
        getImages(data) {
          return this.$store.state.image.image + data ;
        },
        uploadImg(e){
          this.form.img = e;
        },
        parent(e) {
          console.log(e)
        },
        changeAncestor(){
          this.ancestor == true ? this.$refs.ancestor.reset()  : null;
        },
      },
      created() {
        this.loadCategories()
        this.$on('AfterCreate', () => {this.loadCategories()});
      },
      mounted() {
        setTimeout(() => this.loadDescription(), 3000);
      },
      async asyncData({ $axios }) {
        const items = await $axios.$get(`get-men`);
        return { items }
      }
    }
</script>

<style scoped>

</style>

<template>
    <v-container>
      <h2>Добавить пользователя</h2>
      <v-form
        ref="form"
      >
        <v-text-field
          v-model="form.name"
          :counter="10"
          label="Имя"
          required
        ></v-text-field>

        <v-switch
          v-model="ancestor"
          @change="changeAncestor"
          label="Первый Потомок"
        ></v-switch>

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
          @click="submit"
        >
          Отправить
        </v-btn>
      </v-form>
    </v-container>
</template>

<script>
    export default {
        name: "create",
      components: {
        'ckeditor-nuxt': () => import('@blowstack/ckeditor-nuxt')
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
          parent(e) {
            console.log(e)
          },
        async submit() {
          try {
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
            await this.$axios.$post('add-man', formData,config).then(async (e) => {
              this.$toast.success('Публикация успешно создана');

            }).catch(error => {
              this.errors = error.response.data
            })

          }
          catch (e) {
            console.log(e)
          }
        },
        uploadImg(e){
          this.form.img = e;
        },
        changeAncestor(){
           this.ancestor == true ? this.$refs.ancestor.reset()  : null;
        },

      },
      async asyncData({ $axios }) {
        const items = await $axios.$get(`get-men`);
        console.log(items);
        return { items }
      }
    }
</script>

<style scoped>

</style>

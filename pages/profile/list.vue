<template>
  <v-container>
    <v-row class="pa-5">

      <v-col cols="12" md="4" lg="4">
        <v-form>
          <v-text-field
            append-icon="mdi-magnify"
            label="Search"
            single-line
            outlined
            rounded
            dense
            v-model="search"
          ></v-text-field>
        </v-form>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12" md="12" lg="12">
        <v-simple-table>
          <template v-slot:default>
            <thead>
            <tr>
              <th class="text-left">
                №
              </th>
              <th class="text-left">
                Фото
              </th>
              <th class="text-left">
                Имя
              </th>
              <th class="text-left">
                Родитель
              </th>
              <th class="text-left">
                Описание
              </th>
              <th class="text-left">
                Действие
              </th>
            </tr>
            </thead>
            <tbody>
            <tr
              v-for="(item, index) in families"
              :key="item.id"
            >
              <td>{{index + 1}}</td>
              <td><img :src="getImages(item.img)" width="100" height="100"></td>
              <td>{{item.name}}</td>
              <td>{{item.parent_id}}</td>
              <td>{{item.name}}</td>
              <td>
                <v-btn
                  elevation="9"
                  outlined
                  x-small
                  class="text-black"
                  link :to="getData(item.id)"
                >
                  <v-icon x-small color="black" class="mr-2">fa fa-edit</v-icon>
                  Редактировать
                </v-btn>
                <v-btn
                  elevation="9"
                  outlined
                  x-small
                  class="text-black"
                  @click="deleteFamilies(item.id)"
                >
                  <v-icon x-small color="black" class="mr-2">fa fa-trash-alt</v-icon>
                  Удалить
                </v-btn>
              </td>
            </tr>
            </tbody>
          </template>
        </v-simple-table>
        <template>
          <div class="text-center">
            <v-pagination
              v-model="page"
              :length="length"
              :total-visible="7"
              circle
              @input="getPage"
            ></v-pagination>
          </div>
        </template>

      </v-col>
    </v-row>

  </v-container>
</template>

<script>
    export default {
        name: "list",
        data() {
          return {
            page: 1,
            length: 0,
            search: '',
            families: []
          }
        },
      methods: {
          getData(id){
            return '/profile/user/'+id
          },
        loadCategories() {
          this.$axios.get('/families').then(({data}) => (
            [
              // console.log(data.data)
              this.families = data.data,
              this.length = data.last_page,
              this.page = data.current_page
            ]
          ))
        },
        getPage(page) {
          this.$axios.get('/families?page='+page)
            .then(({data}) => {
                this.families = data.data
                this.length = data.last_page
                this.page = data.current_page
            })
            .catch(error => {
              console.log(error)
            })
        },
        getSearch(q) {
          this.$axios.get('/findFamilies?q=' + q)
            .then(({data}) => {
              this.families = data.data
              this.length = data.last_page
              this.page = data.current_page
            })
            .catch(error => {
              console.log(error)
            })
        },
        async deleteFamilies(id) {
          await this.$axios.$delete('families/'+id).then((e) => {console.log(e)})
          this.$toast.success('Пользователь успешно удален')
          this.$emit('AfterCreate');
        },
        getImages(data) {
          return this.$store.state.image.image + data ;
        },
      },
      watch: {
        search: function (e) {
          this.getSearch(e)
        }
      },
      created() {
        this.loadCategories()
        this.$on('AfterCreate', () => {this.loadCategories()});
      },
    }
</script>

<style scoped>

</style>

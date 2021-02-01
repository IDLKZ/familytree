<template>
  <v-container fluid class="py-15" style="background-color: #E5E5E5;">
    <v-row class="px-sm-5">
      <v-col cols="12" md="6" offset-md="3" class="pa-10 my-15 white rounded">
        <div class="text-h4 font-weight-light">
          ACCOUNT LOGIN
        </div>
        <v-form @submit.prevent="submit" class="my-10"
                ref="form"
                lazy-validation
        >
          <v-text-field
            label="Email"
            v-model="form.email"
            required
            type="email"
            outlined
          ></v-text-field>
          <v-text-field
            label="Password"
            :type="hint ? 'text' : 'password'"
            v-model="form.password"
            :append-icon="hint ? 'mdi-eye' : 'mdi-eye-off'"
            @click:append="hint = !hint"
            required
            outlined
          ></v-text-field>
          <v-checkbox
            label="Remember me"
            required
            hint="Forgot password?"
          ></v-checkbox>
          <div class="text-center">
            <v-btn
              rounded
              color="grey darken-4"
              class="mr-4 white--text"
              large
              type="submit"
            >
              Login
            </v-btn>
          </div>


        </v-form>





      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    head: {
      title: 'Login page',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Login page description'
        }
      ],
    },
    name: "login",
    // middleware: 'guest',
    layout:"auth",
    data(){
      return{
        hint:false,
        form:{
          email:"",
          password:""
        }
      }
    },
    methods: {
      async submit() {
        try {
          this.$toast.show('Logging in...')
          await this.$auth.loginWith("local", {
            data: this.form
          })
          this.$toast.success('Successfully authenticated')
        } catch (e) {
          this.$toast.error('Error while authenticating')
          return console.log(e);
        }
        this.$router.push({
          path: this.$route.query.redirect || "/profile"
        })
      }
    }
  }
</script>

<style scoped>

</style>

<template>
  <v-container
    id="user-profile"
    fluid
    tag="section"
  >
    <v-row justify="center">
      <v-col
        cols="12"
        md="8"
      >
        <base-material-card>
          <template v-slot:heading>
            <div class="display-2 font-weight-light">
              Editar Usuario
            </div>
          </template>

          <v-container class="py-0">
            <v-row>
              <v-col
                cols="12"
                md="4"
              >
                <v-text-field
                  v-model="user.username"
                  class="purple-input"
                  label="Username"
                />
              </v-col>

              <v-col
                cols="12"
                md="4"
              >
                <v-text-field
                  v-model="user.email"
                  label="Email"
                  class="purple-input"
                />
              </v-col>

              <v-col
                cols="12"
                md="6"
              >
                <v-text-field
                  v-model="user.name"
                  label="Nombre"
                  class="purple-input"
                />
              </v-col>

              <v-col
                cols="12"
                md="6"
              >
                <v-text-field
                  v-model="user.lastname"
                  label="Apellido"
                  class="purple-input"
                />
              </v-col>
            </v-row>
          </v-container>
          <v-btn @click="updateUser">
            Editar
          </v-btn>
        </base-material-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import axios from 'axios'
  export default {

    data () {
      return {
        user: {
          username: '',
          name: '',
          lastname: '',
          email: '',
        },
      }
    },
    mounted () {
      this.getUserById()
    },
    methods: {
      updateUser () {
        var self = this
        axios.post(this.$store.state.urlApi + '/users/user/' + this.$route.params.id, this.user)
          .then(response => {
            self.$router.push({ path: '/usuarios' })
          })
          .catch(error => {
            console.log(error.response)
          })
      },
      getUserById () {
        axios.get(this.$store.state.urlApi + '/users' + '/' + this.$route.params.id)
          .then(response => {
            this.user = response.data.doc
          })
          .catch(error => {
            console.log(error.response)
          })
      },
    },
  }
</script>

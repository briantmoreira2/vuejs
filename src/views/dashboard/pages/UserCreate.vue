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
              Crear Usuario
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
          <v-btn @click="addUser">
            Crear
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
    methods: {
      addUser () {
        var self = this
        axios.post(this.$store.state.urlApi + '/users/user', this.user)
          .then(response => {
            self.$router.push({ path: '/usuarios' })
          })
          .catch(error => {
            console.log(error.response)
          })
      },
    },
  }
</script>

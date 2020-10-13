<template>
  <v-container
    id="regular-tables"
    fluid
    tag="section"
  >
    <v-btn :to="'/pages/user'">
      Crear Usuario
    </v-btn>
    <base-material-card
      icon="mdi-clipboard-text"
      title="Usuarios"
      class="px-5 py-3"
    >
      <v-simple-table>
        <thead>
          <tr>
            <th class="primary--text">
              Username
            </th>
            <th class="primary--text">
              Nombre
            </th>
            <th class="primary--text">
              Apellido
            </th>
            <th class="primary--text">
              Email
            </th>
            <th class="primary--text">
              Acciones
            </th>
          </tr>
        </thead>

        <tbody>
          <tr
            v-for="(user , i) in users"
            :key="i"
          >
            <td>{{ user.username }}</td>
            <td>{{ user.name }}</td>
            <td>{{ user.lastname }}</td>
            <td>{{ user.email }}</td>
            <td>
              <v-btn :to="'pages/user/edit/' + user._id">
                Editar Usuario
              </v-btn>
              <v-btn @click="delUser(user._id)">
                Borrar Usuario
              </v-btn>
            </td>
          </tr>
        </tbody>
      </v-simple-table>
    </base-material-card>

    <div class="py-3" />
  </v-container>
</template>
<script>
  import axios from 'axios'
  export default {

    data () {
      return {
        users: [],
      }
    },
    mounted () {
      this.getUsers()
    },
    methods: {
      getUsers () {
        axios.get(this.$store.state.urlApi + '/users')
          .then(response => {
            this.users = response.data.doc
            console.log(this.users)
          })
          .catch(error => {
            console.log(error.response)
          })
      },
      delUser (id) {
        var self = this
        axios.post(this.$store.state.urlApi + '/users/user/delete/' + id, this.user)
          .then(response => {
            self.getUsers()
          })
          .catch(error => {
            console.log(error.response)
          })
      },
    },
  }
</script>

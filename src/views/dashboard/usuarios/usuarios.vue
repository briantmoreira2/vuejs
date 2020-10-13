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
      <v-row>
        <v-col
          cols="12"
          sm="6"
          md="3"
        >
          <v-text-field
            v-model="searchUsername"
            label="Buscar"
            placeholder="Usuario"
            outlined
            @input="searchMethod(searchUsername, 'username')"
          />
        </v-col>
        <v-col
          cols="12"
          sm="6"
          md="3"
        >
          <v-text-field
            v-model="searchName"
            label="Buscar"
            placeholder="Nombre"
            outlined
            @input="searchMethod(searchName , 'name')"
          />
        </v-col>
        <v-col
          cols="12"
          sm="6"
          md="3"
        >
          <v-text-field
            v-model="searchLastname"
            label="Buscar"
            placeholder="Apellido"
            outlined
            @input="searchMethod(searchLastname, 'lastname')"
          />
        </v-col>
        <v-col
          cols="12"
          sm="6"
          md="3"
        >
          <v-text-field
            v-model="searchEmail"
            label="Buscar"
            placeholder="Email"
            outlined
            @input="searchMethod(searchEmail , 'email')"
          />
        </v-col>
      </v-row>
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
              <v-row>
                <v-col
                  cols="12"
                  sm="6"
                  md="3"
                >
                  <v-btn
                    style="width: 20px;"
                    :to="'pages/user/edit/' + user._id"
                  >
                    Editar
                  </v-btn>
                </v-col>
                <v-col
                  cols="12"
                  sm="3"
                  md="1"
                />
                <v-col
                  cols="12"
                  sm="6"
                  md="3"
                >
                  <v-btn
                    style="width: 20px;"
                    @click="delUser(user._id)"
                  >
                    Borrar
                  </v-btn>
                </v-col>
              </v-row>
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
        usersAll: [],
        searchName: '',
        searchUsername: '',
        searchLastname: '',
        searchEmail: '',
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
            this.usersAll = this.users
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
      searchMethod (search, valueFilter) {
        console.log(search.toString())
        console.log(valueFilter.toString())
        switch (valueFilter.toString()) {
          case 'name':
            this.users = this.usersAll.filter(rec => rec.name.toString().toUpperCase().search(search.toString().toUpperCase()) !== -1)
            break
          case 'username':
            this.users = this.usersAll.filter(rec => rec.username.toString().toUpperCase().search(search.toString().toUpperCase()) !== -1)
            break
          case 'lastname':
            this.users = this.usersAll.filter(rec => rec.lastname.toString().toUpperCase().search(search.toString().toUpperCase()) !== -1)
            break
          case 'email':
            this.users = this.usersAll.filter(rec => rec.email.toString().toUpperCase().search(search.toString().toUpperCase()) !== -1)
            break
        }
        if (search === '') {
          this.users = this.usersAll
        }
      },
    },
  }
</script>

<template>
  <v-app dark>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-toolbar-title v-text="title" />
      <v-spacer />
      
      <v-btn icon v-if="logged && role === 'reporter'">
        <v-icon>mdi-pencil-plus</v-icon>
      </v-btn>
      <!-- Avatar do usuário -->
      <v-menu
        v-model="rightDrawer"
        absolute
        :close-on-content-click="false"
        :position-y="60"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            icon
            v-bind="attrs"
            v-on="on"
            @click.stop="rightDrawer = !rightDrawer"
          >
            <v-avatar>
              <v-icon v-if="logged">mdi-account-circle</v-icon>
              <v-icon v-else>mdi-login-variant</v-icon>
            </v-avatar>
          </v-btn>  
        </template>
        <v-card min-width="300" v-if="!logged && !notRegister">
          <v-card-text>
            <v-text-field
              v-model="email"
              type="text"
              name="input-10-2"
              label="Email"
            ></v-text-field>
            <v-text-field
            v-model="password"
              :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
              :type="show ? 'text' : 'password'"
              name="input-10-2"
              label="Senha"
              @click:append="show = !show"
            ></v-text-field>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              text
              @click="notRegister = !notRegister"
            >
              Registrar
            </v-btn>
            <v-btn
              v-if="!logged"
              color="primary"
              text
              @click="login"
            >
              Entrar
            </v-btn>
          </v-card-actions>
        </v-card>
        <v-card min-width="300" v-if="logged && !notRegister">
          <v-card-text>
            <div class="mx-auto text-center">
              <v-avatar
                color="brown"
              >
                <span class="white--text text-h5"></span>
              </v-avatar>
              <h3>{{ name }}</h3>
              <v-divider class="my-3"></v-divider>
              <p>
                {{ role }}
              </p>
              <v-divider class="my-3"></v-divider>
              <p>
                {{ email }}
              </p>
              <div v-if="role === 'diretor' || role === 'dev'">
                <v-divider class="my-3"></v-divider>
                <v-btn
                  rounded
                  variant="text"
                  to="/about"
                  @click.stop="rightDrawer = !rightDrawer"
                >
                  Gerenciamento
                </v-btn>
              </div>
              <div v-else>
                <v-divider class="my-3"></v-divider>
                <v-btn
                  rounded
                  variant="text"
                  to="/about"
                >
                  Minha conta
                </v-btn>
              </div>
              <v-divider class="my-3"></v-divider>
              <v-btn
                rounded
                variant="text"
                @click="logout"
              >
                Sair
              </v-btn>
            </div>
          </v-card-text>
        </v-card>
        <v-card min-width="300" v-if="notRegister && !logged">
          <v-card-text>
            <div class="mx-auto text-center">
              <h3>Registre-se</h3>
              <v-divider class="my-3"></v-divider>
              <v-text-field
                v-model="registering.name"
                type="text"
                name="input-10-2"
                label="Nome"
            ></v-text-field>
              <v-divider class="my-3"></v-divider>
              <v-text-field
                v-model="registering.email"
                type="text"
                name="input-10-2"
                label="Email"
            ></v-text-field>
              <v-divider class="my-3"></v-divider>
              <v-text-field
                v-model="registering.password"
                :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
                :type="show ? 'text' : 'password'"
                name="input-10-2"
                label="Senha"
                @click:append="show = !show"
            ></v-text-field>
              <v-divider class="my-3"></v-divider>
              <v-select
                :items="list"
                item-text="name"
                item-value="id"
                label="Cargos"
                @change="setRole"
            ></v-select>
              <v-divider class="my-3"></v-divider>
              <v-btn
                rounded
                variant="text"
                @click="notRegister = !notRegister"
              >
                Voltar
              </v-btn>
              <v-btn
                rounded
                variant="text"
                @click="register"
              >
                Registrar
              </v-btn>
            </div>
          </v-card-text>
        </v-card>
      </v-menu>
    </v-app-bar>
    <v-main>
      <v-container fluid>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      registering: {
        name: null,
        email: null,
        password: null,
        role: null
      },
      notRegister: false,
      role: null,
      list: [],
      name: null,
      logged: false,
      email: null,
      password: null,
      clipped: true,
      drawer: false,
      fixed: false,
      show: false,
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Jornal'
    }
  },
  methods: {
    async login(){
      await this.$axios.$post('login', {
        email: this.email,
        password: this.password
      }).then(res => {
        sessionStorage.setItem('token', res.access_token)
        sessionStorage.setItem('user_name', res.user.name)
        sessionStorage.setItem('user_role', res.role)
        sessionStorage.setItem('user_email', this.email)
        this.$axios.setToken(res.access_token, 'Bearer')
        this.name = res.user.name
        this.role = res.role
        this.logged = !this.logged
      })
    },
    async register(){
      await this.$axios.$post('register', {
        name: this.registering.name,
        email: this.registering.email,
        password: this.registering.password,
        role: this.registering.role
      })

      this.notRegister = !this.notRegister
    },
    async roleList(){
      let obj = {
        id: null,
        name: null
      }
      await this.$axios.$get('role').then(res => {
        for(let i = 0; i < res.length; i++)
          this.list[i] = res[i]
      })
    },
    async logout(){
      sessionStorage.removeItem('token')
      await this.$axios.$post('logout')
      this.logged = !this.logged
    },
    async setRole(value){
      this.registering.role = value
    }
  },
  mounted(){
    if(sessionStorage.getItem('token')){
      this.$axios.setToken(sessionStorage.getItem('token'), 'Bearer')
      this.name = sessionStorage.getItem('user_name')
      this.role = sessionStorage.getItem('user_role')
      this.email = sessionStorage.getItem('user_email')
      this.logged = !this.logged
    }
    this.roleList()
  }
}
</script>

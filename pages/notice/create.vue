<template>
  <v-card flat>
    <v-snackbar v-model="snackbar" absolute top right color="success">
      <span>Registration successful!</span>
      <v-icon dark> mdi-checkbox-marked-circle </v-icon>
    </v-snackbar>
    <v-form ref="form" @submit.prevent="submit">
      <v-container fluid>
        <v-row>
          <v-col cols="12" sm="6">
            <v-text-field
              v-model="form.title"
              clearable
              color="purple darken-2"
              label="Título"
            ></v-text-field>
          </v-col>
          <v-col cols="12" sm="6">
            <v-text-field
              v-model="form.description"
              clearable
              color="blue darken-2"
              label="Descrição"
            ></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-textarea clearable v-model="form.content" color="teal">
              <template v-slot:label>
                <div>Conteúdo</div>
              </template>
            </v-textarea>
          </v-col>
          <v-col cols="12" sm="6">
            <v-select
              v-model="form.status"
              :items="categories"
              item-text="name"
              item-value="id"
              clearable
              color="pink"
              label="Categoria"
            ></v-select>
          </v-col>
        </v-row>
      </v-container>
      <v-card-actions>
        <v-btn text to="/"> Voltar </v-btn>
        <v-btn text @click="resetForm"> Limpar </v-btn>
        <v-spacer></v-spacer>
        <v-btn text color="primary" type="submit">
          Register
        </v-btn>
      </v-card-actions>
    </v-form>
  </v-card>
</template>
<script>

  export default {
    data () {
      return {
        form: { title: null, description: null, content: null, status: null, user: null },
        categories: null,
        snackbar: false
      }
    },
    methods: {
      resetForm () {
        this.form = {}
      },
      async submit () {
        await this.$axios.$post('notice', {
            title: this.form.title,
            description: this.form.description,
            body: this.form.content,
            status_id: this.form.status,
            user_id: this.form.user
        }).finally(() => {
            this.snackbar = !this.snackbar
        })
      }
    },
    async mounted(){
        this.form.user = JSON.parse(sessionStorage.getItem('user_id'))
        if(!this.categories)
            await this.$axios.$get('status').then(res => this.categories = res)
    }
  }
</script>

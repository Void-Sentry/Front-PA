<template>
  <v-dialog width="1200" @input="close(dialog)" v-model="dialog" :close-on-content-click="!dialog">
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
                label="Abordagem geral"
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-textarea clearable v-model="form.body" color="teal">
                <template v-slot:label>
                  <div>Conteúdo</div>
                </template>
              </v-textarea>
            </v-col>
            <v-col cols="12" sm="6">
              <v-select
                v-model="form.status_id"
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
          <v-btn text color="error" @click.stop="destroy"> Excluir </v-btn>
          <v-btn text color="primary" type="submit"> Atualizar </v-btn>
        </v-card-actions>
      </v-form>
    </v-card>
  </v-dialog>
</template>
<script>
export default {
  name: "EditNotice",
  props: {
    data: Object,
  },
  data() {
    return {
      form: {
        title: null,
        description: null,
        body: null,
        status_id: null,
        user_id: null,
      },
      categories: null,
      snackbar: false,
      dialog: false,
    };
  },
  methods: {
    resetForm() {
      this.form = {};
    },
    async submit() {
      await this.$axios
        .$put(`notice/${this.form.id}`, {
          title: this.form.title,
          description: this.form.description,
          body: this.form.body,
          status_id: this.form.status_id,
          user_id: this.form.user_id,
        })
        .finally(() => {
          this.snackbar = !this.snackbar;
        });
    },
    close(value){
      if(!value)
        this.$emit('closeEdit')
    },
    async destroy(){
      await this.$axios.$delete(`notice/${this.form.id}`)
      this.dialog = !this.dialog
      this.$emit('destroyNotice')
    }
  },
  async mounted() {
    this.form = this.$props.data;
    this.dialog = !this.dialog
    this.form.user_id = JSON.parse(sessionStorage.getItem("user_id"));
    if (!this.categories)
      await this.$axios.$get("status").then((res) => (this.categories = res));
  },
};
</script>

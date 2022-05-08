<template>
    <div class="text-center">
      <v-dialog
        v-model="dialog"
        v-click-outside="fechar"
        activator="parent"
      >
        <v-card>
          <v-card-text>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
          </v-card-text>
          <v-card-actions>
            <v-btn color="primary" block @click="dialog = false">Close Dialog</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
  </div>
</template>
<script>
export default {
    name: 'ExibirNoticia',
    props: {
        data: Object
    },
    data() {
        return {
            dialog: false
        }
    },
    methods: {
        fechar(){
            this.dialog = !this.dialog
            this.$emit('closeModal')
        }
    },
    mounted(){
        this.dialog = !this.dialog
    }
}
</script>

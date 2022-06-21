<template>
  <v-dialog @input="close(dialog)" v-model="dialog" :close-on-content-click="!dialog">
    <v-card>
      <v-card-title>
        {{ this.$props.data.title }}
      </v-card-title>
      <v-card-subtitle>
        {{ new Date(this.$props.data.created_at) }}
      </v-card-subtitle>
      <v-card-subtitle class="text-center">
        {{ this.$props.data.description }}
      </v-card-subtitle>
      <v-card-text>
        <v-textarea v-model="$props.data.body">
        </v-textarea>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>
<script>
export default {
  name: "ExibirNoticia",
  props: {
    data: Object
  },
  data() {
    return {
      dialog: false
    };
  },
  methods: {
    close(dialog){
      if(!dialog)
        this.$emit("closeModal");
    }
  },
  mounted() {
    this.dialog = !this.dialog;
  },
};
</script>

<template>
  <div>
    <v-parallax
      height="300"
      src="https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fwww.pixelstalk.net%2Fwp-content%2Fuploads%2F2016%2F03%2FDark-wallpaper-Veins-Detail.jpg&f=1&nofb=1"
    >
      <div class="d-flex flex-column fill-height justify-center align-center text-white">
        <h1 class="text-h4 font-weight-thin mb-4">
          Nome da Empresa
        </h1>
        <h4 class="subheading">
          Alguma frase de efeito para marketing
        </h4>
      </div>
    </v-parallax>
    
    <v-row>
      <v-col v-for="item in notices" :key="item.id">
        <v-card class="mx-auto" max-width="344">
          <v-img
            src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
          ></v-img>

          <v-card-title>
            {{ item.title }}
          </v-card-title>

          <v-card-actions>
            <v-btn color="orange-lighten-2" variant="text" @click="openning(item)">
              Explore
            </v-btn>

            <v-spacer></v-spacer>

            <v-btn @click="item.show = !item.show">
              <v-icon>{{
                item.show ? "mdi-chevron-up" : "mdi-chevron-down"
              }}</v-icon>
            </v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="item.show">
              <v-divider></v-divider>

              <v-card-text>
                {{ item.description }}
              </v-card-text>
            </div>
          </v-expand-transition>
        </v-card>

        <div v-if="open">
          <open-modal @closeModal="open = !open" :data="object"></open-modal>
        </div>
      </v-col>
    </v-row>
</div>
</template>

<script>
import openModal from "@/components/show.vue";

export default {
  name: "Index",
  components: {
    openModal,
  },
  data() {
    return {
      notices: [],
      open: false,
      object: null
    };
  },
  methods: {
    async getNotices() {
      await this.$axios.get("notice").then((res) => {
        this.notices = res.data.filter((arr) => {
          arr.show = false;
          return arr;
        });
      });
    },
    openning(value){
      console.log(value)
      this.open = !this.open
      this.object = value
    }
  },
  mounted() {
    this.getNotices();
  },
};
</script>
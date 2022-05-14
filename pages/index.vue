<template>
  <div>
    <v-parallax
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

    <v-row class="justify-center">
      <v-col cols="3">
        <v-autocomplete
          v-model="input"
          :items="notices"
          :search-input.sync="search"
          color="white"
          hide-no-data
          hide-selected
          clearable
          @change="openning"
          item-text="title"
          item-value="id"
          label="Ache notícias do seu interesse!"
          prepend-icon="mdi-magnify"
          return-object
        ></v-autocomplete>
      </v-col>
    </v-row>
      
    <v-row class="justify-center">
      <div v-for="index in categories" :key="index.id">
        <v-chip>{{ index.name }}</v-chip>
      </div>
      <v-btn icon @click.stop="openStatusCreator = !openStatusCreator"><v-icon>mdi-plus</v-icon></v-btn>
      <div v-if="openStatusCreator">
        <create-status @closeStatusCreator="openStatusCreator = !openStatusCreator"></create-status>
      </div>
    </v-row>
    
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
            <v-btn v-if="item.user_id === user_id" color="orange-lighten-2" variant="text" @click.stop="edit(item)">
              Editar
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
      </v-col>
      <div v-if="openShow">
        <show-modal @closeModal="openShow = !openShow" :data="object"></show-modal>
      </div>
      <div v-if="openEdit">
        <edit-modal @closeEdit="openEdit = !openEdit" @destroyNotice="getNotices" :data="object"></edit-modal>
      </div>
    </v-row>
</div>
</template>

<script>
// Notice manager
import showModal from "~/components/notice/show.vue";
import editModal from "~/components/notice/edit.vue";

// Status manager
import createStatus from "~/components/status/create.vue";

export default {
  name: "Index",
  components: {
    showModal,
    editModal,
    createStatus
  },
  data() {
    return {
      notices: [],
      openEdit: false,
      openShow: false,
      object: null,
      categories: null,
      input: null,
      search: null,
      user_id: null,
      openStatusCreator: false,
    };
  },
  methods: {
    async getNotices() {
      await this.$axios.get("notice").then((res) => {
        this.notices = res.data.filter((arr) => {
          arr.show = false;
          return arr;
        });
      })
    },
    async getCategories(){
      await this.$axios.get('status').then(res => {
        this.categories = res.data
      })
    },
    openning(value){
      if(value){
        this.openShow = !this.openShow
        this.object = value
      }
    },
    edit(value){
      if(value){
        this.openEdit = !this.openEdit
        this.object = value
      }
    }
  },
  mounted() {
    this.getNotices();
    this.getCategories();
    if(sessionStorage.getItem('user_id'))
      this.user_id = JSON.parse(sessionStorage.getItem('user_id'))
  },
};
</script>
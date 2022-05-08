<template>
    <v-row>
      <v-col v-for="notice in notices" :key="notice.id">
        <v-card class="mx-auto" max-width="344">
          <v-img
            src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
            height="200px"
            cover
          ></v-img>

          <v-card-title>
            {{ notice.title }}
          </v-card-title>

          <v-card-actions>
            <v-btn color="orange-lighten-2" variant="text" @click="open = !open">
              Explore
            </v-btn>

            <v-spacer></v-spacer>

            <v-btn @click="notice.show = !notice.show">
              <v-icon>{{
                notice.show ? "mdi-chevron-up" : "mdi-chevron-down"
              }}</v-icon>
            </v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="notice.show">
              <v-divider></v-divider>

              <v-card-text>
                {{ notice.description }}
              </v-card-text>
            </div>
          </v-expand-transition>
        </v-card>
        <div v-if="open">
          <open-modal @closeModal="open = !open" :data="notice"></open-modal>
        </div>
      </v-col>
    </v-row>
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
    }
  },
  mounted() {
    this.getNotices();
  },
};
</script>
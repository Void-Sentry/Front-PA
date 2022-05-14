<template>
  <v-card>
    <v-container>
      <v-row>
        <v-col cols="2" v-if="user_role === 'diretor'">
            <v-list shaped>
              <v-subheader>Configurações</v-subheader>
              <v-list-item-group
                v-model="selectedItem"
              >
                <v-list-item
                  v-for="(item, i) in items"
                  :key="i"
                  :to="item.to"
                >
                  <v-list-item-icon>
                    <v-icon v-text="item.icon"></v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title v-text="item.text"></v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
              </v-list-item-group>
            </v-list>
        </v-col>
        <v-col cols="2" v-else>
            <v-list shaped>
              <v-subheader>Configurações</v-subheader>
              <v-list-item-group
                v-model="selectedItem"
              >
                <v-list-item
                  v-for="(item, i) in items"
                  :key="i"
                  :to="item.to"
                >
                  <v-list-item-icon>
                    <v-icon v-text="item.icon"></v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title v-text="item.text"></v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
              </v-list-item-group>
            </v-list>
        </v-col>
        <profile />
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
  import profile from '@/components/user/profile.vue'

  export default {
    name: 'Gerenciamento',
    components: {
      profile
    },
    data: () => ({
      selectedItem: 1,
      user_role: null,
      items: [
        { text: 'Perfil', icon: 'mdi-account-details' },
        { text: 'Usuários', icon: 'mdi-account-group' },
        { text: 'Estatística', icon: 'mdi-chart-bar' },
        { text: 'Voltar', icon: 'mdi-close', to: '/' },
      ],
    }),
    mounted(){
      this.user_role = sessionStorage.getItem('user_role')
    }
  }
</script>

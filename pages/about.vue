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
                  @click.stop="changeViews(item.text)" 
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
        <div v-if="profileView">
          <profile />
        </div> 
        <div v-if="userView">
          <v-row style="width:70vw;">
            <v-col>
              <user />
            </v-col>
            <v-col class="justify-end">
              <v-btn icon>
                    <v-icon>mdi-plus</v-icon>
              </v-btn>
            </v-col>
          </v-row>
        </div> 
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
  import profile from '@/components/user/profile.vue'
  import user from '@/components/user/user.vue'

  export default {
    name: 'Gerenciamento',
    components: {
      profile,
      user
    },
    data () {
      return {
        selectedItem: 1,
        userView: false,
        profileView: false,
        estatiscaView: false,
        user_role: null,
        items: [
          { text: 'Perfil', icon: 'mdi-account-details' },
          { text: 'Usuários', icon: 'mdi-account-group' },
          { text: 'Estatística', icon: 'mdi-chart-bar' },
          { text: 'Voltar', icon: 'mdi-close', to: '/' },
        ],
      }  
    },
    methods: {
      changeViews(text){
        switch(text){
          case 'Perfil':
            this.profileView = !this.profileView
            this.userView = false
            this.estatiscaView = false
          break
          case 'Usuários':
             this.userView = !this.userView
             this.estatiscaView = false
             this.profileView = false
          break
          case 'Estatística':
             this.estatiscaView = !this.estatiscaView
             this.profileView = false
             this.userView = false 
          break
        }
      }
    },
    mounted(){
      this.user_role = sessionStorage.getItem('user_role')
    }
  }
</script>

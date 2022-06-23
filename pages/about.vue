<template>
  <v-card>
    <v-container>
      <v-row>
        <v-col cols="2">
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
        <v-col>
          <div v-if="profileView">
            <profile />
          </div>
          <div v-if="userView">
            <user />
          </div>
          <div v-if="noticeView">
            <notice />
          </div>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
  import profile from '@/components/user/profile.vue'
  import user from '@/components/user/user.vue'
  import notice from '@/components/notice/admNotice.vue'

  export default {
    name: 'Gerenciamento',
    components: {
      profile,
      user,
      notice
    },
    data () {
      return {
        selectedItem: 1,
        userView: false,
        profileView: false,
        estatiscaView: false,
        noticeView: false,
        user_role: null,
        items: [
          { text: 'Perfil', icon: 'mdi-account-details' },
          { text: 'Usuários', icon: 'mdi-account-group' },
          { text: 'Estatística', icon: 'mdi-chart-bar' },
          { text: 'Noticias', icon: 'mdi-playlist-check'},
          { text: 'Voltar', icon: 'mdi-close', to: '/' }
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
            this.noticeView = false
          break
          case 'Usuários':
             this.userView = !this.userView
             this.estatiscaView = false
             this.profileView = false
             this.noticeView = false
          break
          case 'Estatística':
             this.estatiscaView = !this.estatiscaView
             this.profileView = false
             this.userView = false 
             this.noticeView = false
          break
          case 'Noticias':
             this.noticeView = !this.noticeView
             this.profileView = false
             this.userView = false 
             this.estatiscaView = false
          break
        }
      }
    },
    mounted(){
      this.user_role = sessionStorage.getItem('user_role')
    }
  }
</script>

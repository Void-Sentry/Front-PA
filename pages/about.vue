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
            <v-row>
              <v-col>
                <v-avatar class="profile" color="grey" size="64" tile>
                </v-avatar>
              </v-col>
            </v-row>
            <v-row>
              <v-col>
                <v-text-field label="Nome completo"></v-text-field>
              </v-col>
              <v-col>
                <v-text-field label="Email"></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col>
                <v-text-field label="Senha atual"> </v-text-field>
              </v-col>
              <v-col>
                <v-text-field
                  label="Nova senha"
                  required
                  placeholder="Digite a sua nova senha"
                ></v-text-field>
              </v-col>
              <v-col>
                <v-text-field
                  label="Confirme sua nova senha"
                  required
                  placeholder="Confirme a sua nova senha"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-btn small>
                Salvar alterações
              </v-btn>
              <v-btn small> Limpar campos </v-btn>
            </v-row>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
  export default {
    name: 'Sobre',
    data: () => ({
      selectedItem: 1,
      items: [
        { text: 'Perfil', icon: 'mdi-account' },
        { text: 'Audience', icon: 'mdi-clock' },
        { text: 'Conversions', icon: 'mdi-flag' },
      ],
    }),
  }
</script>

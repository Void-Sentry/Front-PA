<template>
  <div class="page">
    <template>
      <!-- <div
        cols="12"
        style="width: 100%"
        :class="
          $vuetify.breakpoint.xsOnly
            ? 'container-fluid pl-5 pt-6 pb-2'
            : 'container-fluid pl-12 pt-6 pb-2'
        "
      >
        <span style="font-weight: bolder">Minha conta</span>
        <v-divider
          vertical
          class="mx-4"
          color="black"
          style="display: inline; opacity: 0.3"
        ></v-divider>
        <v-icon color="primary" class="pb-1" dense> mdi-home-outline </v-icon>
        <v-icon class="pb-1 mx-2"> mdi-chevron-right </v-icon>
        <span style="color: #1976d2; font-weight: bolder">Meus dados</span>
        <v-icon class="pb-1 mx-2"> mdi-chevron-right </v-icon>
        <span style="color: #1976d2; font-weight: bolder"></span>
      </div> -->
      <!-- <v-card
        style="float: left"
        :class="
          $vuetify.breakpoint.xsOnly
            ? 'pl-4 pt-2'
            : 'pa-12 pt-0 mt-2 col-md-4 col-sm-5'
        "
        flat
      >
        <v-navigation-drawer floating permanent>
          <v-list dense rounded>
            <v-list-item
              link
            >
              <v-list-item-icon>
                <v-icon color="white"></v-icon>
              </v-list-item-icon>

              <v-list-item-icon>
                <v-icon></v-icon>
              </v-list-item-icon>

              <v-list-item-content>
                <v-list-item-title class="white--text" color="white">
                </v-list-item-title>
              </v-list-item-content>

              <v-list-item-content>
                <v-list-item-title></v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-navigation-drawer>
      </v-card> -->
      <v-card
        style="float: left"
        :class="
          $vuetify.breakpoint.xsOnly
            ? 'pa-2 pt-0 mt-0 col-12'
            : 'pa-2 pt-0 col-md-7 mt-4 col-sm-7'
        "
      >
        <v-form
          ref="formEmail"
          lazy-validation
        >
          <v-container>
            <v-row>
              <v-col cols="2">
                <v-avatar class="profile" color="grey" size="64" tile>
                  <!-- <v-img
                  ></v-img> -->
                </v-avatar>
              </v-col>
              <v-col cols="10">
                <v-row class="mt-2 pl-2">
                  <v-btn
                    cols="6"
                    style="text-transform: none"
                    color="primary"
                    small
                    elevation="2"
                    class="mr-4 ml-4"
                  >
                    <v-icon right dark> mdi-cloud-upload </v-icon>
                  </v-btn>
                  <input
                    ref="uploader"
                    class="d-none"
                    type="file"
                    accept="image/jpeg, image/jpg"
                    id="uploader"
                  />
                  <v-btn
                    style="text-transform: none"
                    elevation="2"
                    small
                    outlined
                    color="primary"
                  >
                    <span>Atualizar</span>
                    <v-icon> mdi-sync </v-icon>
                    <v-icon> mdi-sync </v-icon>
                  </v-btn>
                </v-row>
                <v-row class="mt-2 pl-2">
                  <span class="text--secondary ml-4" style="font-size: 0.9em">
                    Fotos permitidas com extensão .jpg ou .jpeg
                  </span>
                </v-row>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6" class="pt-0 pb-0">
                <v-text-field
                  label="Nome completo"
                ></v-text-field>
              </v-col>
              <v-col cols="6" class="pt-0 pb-0">
                <v-text-field
                  label="Email"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="Senha atual"
                >
                </v-text-field>
              </v-col>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="Nova senha"
                  required
                  placeholder="Digite a sua nova senha"
                ></v-text-field>
              </v-col>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="Confirme sua nova senha"
                  required
                  placeholder="Confirme a sua nova senha"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <!-- <v-alert
                dense
                class="ml-2 text--primary"
                border="left"
                type="warning"
              >
                Por favor, verifique o seu endereço de
                <strong>email</strong> para confirmar as informações registradas
              </v-alert> -->
            </v-row>
            <v-row class="pt-0 pb-2">
              <v-btn
                color="primary"
                small
                class="mr-4 ml-2"
              >
                Salvar alterações
              </v-btn>
              <v-btn
                small
                outlined
                color="primary"
              >
                Limpar campos
              </v-btn>
            </v-row>
          </v-container>
        </v-form>
        <!-- <v-form
          ref="formSenha"
        >
          <v-container>
            
            <v-row class="pt-0 pb-2">
              <v-btn
                color="primary"
                small
                class="mr-4 ml-2"
              >
                Salvar alterações
              </v-btn>
              <v-btn
                small
                outlined
                color="primary"
              >
                Limpar campos
              </v-btn>
            </v-row>
          </v-container>
        </v-form> -->
        <!-- <v-form ref="formInfo" lazy-validation>
          <v-container>
            <v-row>
              <v-col cols="6" class="pt-2 pb-0">
                <v-text-field
                  label="Nome completo"
                  disabled
                ></v-text-field>
              </v-col>
              <v-col cols="6" class="pt-2 pb-0">
                <v-text-field
                  label="Email"
                  disabled
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6" class="pt-0 pb-0">
                <v-text-field
                  label="Nome da mãe"
                  disabled
                ></v-text-field>
              </v-col>
              <v-col cols="6" class="pt-0 pb-0">
                <v-text-field
                  label="Nome do pai"
                  disabled
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="CPF"
                  disabled
                ></v-text-field>
              </v-col>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="Número do RG"
                ></v-text-field>
              </v-col>
              <v-col cols="4" class="pt-0 pb-0">
                <v-menu
                  :close-on-content-click="false"
                  :nudge-right="40"
                  transition="scale-transition"
                  offset-y
                  min-width="290px"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      label="Data de Nascimento"
                      readonly
                      v-bind="attrs"
                      v-on="on"
                      type="date"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                  ></v-date-picker>
                </v-menu>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="CEP"
                ></v-text-field>
              </v-col>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="Cidade"
                ></v-text-field>
              </v-col>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="Bairro"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6" class="pt-0 pb-0">
                <v-text-field
                  label="Endereço"
                ></v-text-field>
              </v-col>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="Complemento"
                ></v-text-field>
              </v-col>
              <v-col cols="2" class="pt-0 pb-0">
                <v-text-field
                  label="Numero"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="Telefone 1"
                ></v-text-field>
              </v-col>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="Telefone 2"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="4" class="pt-0 pb-0">
                <v-text-field
                  label="Telefone 3"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row class="pt-0 pb-2">
              <v-btn
                color="primary"
                small
                class="mr-4 ml-2"
              >
                Salvar alterações
              </v-btn>
              <v-btn
                small
                outlined
                color="primary"
              >
                Limpar campos
              </v-btn>
            </v-row>
          </v-container>
        </v-form> -->
      </v-card>
    </template>
  </div>
</template>

<template>
    <v-col>
        <v-row>
            <v-col>
            <v-avatar class="profile" color="grey" size="64" tile>
            </v-avatar>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
            <v-text-field v-model="name" label="Nome" readonly></v-text-field>
            </v-col>
            <v-col>
            <v-text-field v-model="email" label="Email" readonly></v-text-field>
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
</template>
<script>
export default {
    data() {
        return {
            name: null,
            email: null
        }
    },
    mounted(){
        this.name = sessionStorage.getItem('user_name')
        this.email = sessionStorage.getItem('user_email')
    }
}
</script>

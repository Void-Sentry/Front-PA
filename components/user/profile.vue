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
            <v-text-field v-model="name" label="Nome"></v-text-field>
            </v-col>
            <v-col>
            <v-text-field v-model="email" label="Email"></v-text-field>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
            <v-text-field v-model="current" label="Senha atual"> </v-text-field>
            </v-col>
            <v-col>
            <v-text-field 
                v-model="newpassword"
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
            <v-btn small @click.stop="edit_user_prop">
            Salvar alterações
            </v-btn>
            <v-btn small > Limpar campos </v-btn>
        </v-row>
    </v-col>
</template>
<script>
export default {
    data() {
        return {
            id: sessionStorage.getItem("user_id"),
            current: null,
            newpassword: null,
            name: null,
            email: null
        }
    },
    methods:{
        async edit_user_prop(){
            await this.$axios.$put(`user/${this.id}`, {
                name: this.name,
                email: this.email,
                password: this.current,
                newpassword: this.newpassword
            })
        }
    },
    mounted(){
        this.name = sessionStorage.getItem('user_name')
        this.email = sessionStorage.getItem('user_email')
    }
}
</script>

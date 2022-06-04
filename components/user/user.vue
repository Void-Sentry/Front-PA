<template>
    <div>
        <v-data-table
            :items="list_user"
            :headers="headers">
            <template v-slot:[`item.actions`]='{ item }'>
                <v-icon
                    @click.stop="edit_user(item)">
                    mdi-account-edit-outline
                </v-icon>
                <v-icon
                    @click.stop="delete_user(item)">
                    mdi-delete-forever-outline
                </v-icon>
            </template>
        </v-data-table> 
        <div v-if="popup">
            <v-dialog width="800" v-model="popup" :close-on-content-click="!popup">
                <v-card min-width="300">
                    <v-card-text>
                        <div class="mx-auto text-center">
                        <h3>Editar Usuário(a)</h3>
                        <v-divider class="my-3"></v-divider>
                        <v-text-field
                            v-model="item.name"
                            type="text"
                            name="input-10-2"
                            label="Nome"
                        ></v-text-field>
                        <v-divider class="my-3"></v-divider>
                        <v-text-field
                            v-model="item.email"
                            type="text"
                            name="input-10-2"
                            label="Email"
                        ></v-text-field>
                        <v-divider class="my-3"></v-divider>
                        <v-select
                            :items="listCargos"
                            item-text="name"
                            item-value="id"
                            label="Cargos"
                            v-model="item.role_id"
                        ></v-select>
                        <v-divider class="my-3"></v-divider>
                        <v-btn
                            rounded
                            variant="text"
                            @click.stop="edit"
                        >
                            Editar
                        </v-btn>
                        </div>
                    </v-card-text>
                </v-card>
            </v-dialog>
        </div>
    </div>
    
</template>

<script>
   export default {
       data(){
           return {
               listCargos:null,
               item:null,
               popup:false,
               list_user:[],
               headers: [ 
                    { text: 'Nome', value: 'name', width: '31%' }, 
                    { text: 'Email', value: 'email', width: '30%' }, 
                    { text: 'Cargos', value: 'cargo', width: '30%'},
                    { text: 'Ações', value: 'actions' }  
                ]
           }
       },
        methods: {
            edit_user(user){
                this.item=user
                this.popup=!this.popup
            },
            edit(){
                this.$axios.$put(`user/${this.item.id}`, {
                    name:this.item.name,
                    email:this.item.email,
                    role_id:this.item.role_id
                })
            },
            async delete_user(user){
                await this.$axios.$delete(`user/${user.id}`)
                 this.index()    
            },
            async index(){
                await this.$axios.$get("user/list/role").then(response=>{
                    this.list_user=response
                })  
            }
        },
        async mounted(){
            this.index()
            await this.$axios.$get("role").then(response =>{
                this.listCargos=response
            })
        }     
   } 
</script>
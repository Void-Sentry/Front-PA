<template>
    <div>
        <v-data-table
            :items="list_notice"
            :headers="headers">
            <template v-slot:[`item.actions`]='{ item }'>
                <v-icon
                    @click.stop="to_approve(item)">
                    mdi-eye-check-outline
                </v-icon>
            </template>
        </v-data-table> 
        <div v-if="popup">
            <v-dialog width="800" v-model="popup" :close-on-content-click="!popup">
                <v-card min-width="300">
                    <v-card-text>
                        <div class="mx-auto text-center">
                            <h3>Gerenciamento Noticias</h3>
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
                                    v-model="item.cargo"
                                    type="text"
                                    name="input-10-2"
                                    label="Cargo"
                                ></v-select>
                            <v-divider class="my-3"></v-divider>
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
               listNotice:null,
               item:null,
               popup:false,
               list_notice:[],
               headers: [ 
                    { text: 'Titulo', value: 'title', width: '31%' }, 
                    { text: 'Autor', value: 'name', width: '30%' }, 
                    { text: 'Cargo', value: 'cargo', width: '30%'},
                    { text: 'Pendente', value: 'actions' }  
                ]
           }
       },
       methods: {
            async to_approve(item){
                await this.$axios.$patch(`notice/${item.id}`)
                this.index()    
            },
            async index(){
                await this.$axios.$get("notice/list/notice/state").then(response =>{
                    this.listNotice=response
                }) 
            }
        },
        async mounted(){
            await this.$axios.$get("notice/list/notice/state").then(response =>{
                this.list_notice=response
            })
        }     
   } 
</script>
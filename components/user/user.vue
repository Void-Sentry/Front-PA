<template>
    <div>
        <v-list dense>
            <v-list-item-group
                color="primary"
            >
                <v-subheader>Lista De Usuários</v-subheader>
                <v-list-item
                v-for="(item, i) in list_User"
                :key="i"
                >
                <v-list-item-content>
                    <v-list-item-title v-text="item.name"></v-list-item-title>
                </v-list-item-content>
                <v-btn icon>
                    <v-icon>mdi-delete-forever-outline</v-icon>
                </v-btn> 
                <v-btn icon>
                    <v-icon>mdi-account-edit-outline</v-icon>
                </v-btn> 
                </v-list-item>
            </v-list-item-group>
        </v-list>
    </div>
</template>

<script>
   export default {
       data(){
           return {
               list_User:[]
           }
       },
        async mounted(){
            await this.$axios.$get("user").then(response =>{
                this.list_User=response
            })
        }     
   } 
</script>
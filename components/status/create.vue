<template>
    <v-dialog width="300" @input="close(dialog)" v-model="dialog" :close-on-content-click="!dialog">
        <v-text-field >
            aaaa
        </v-text-field>
    </v-dialog>
</template>
<script>
export default {
    data() {
        return {
            text: null,
            dialog: false
        }
    },
    methods: {
        close(dialog){
            if(!dialog){
                this.$emit('closeStatusCreator')
            }
        }
    },
    mounted(){
        this.dialog = !this.dialog
        console.log(this.dialog)
    }
}
</script>

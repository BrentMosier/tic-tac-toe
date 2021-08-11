<template>
    <v-card variant="outlined">
        <v-card-text class=text-center v-bind:style="[this.move != '' ? this.move === 'X' ? {'color':'green' }:{'color':'red' } : {'color':'black' }]">
            <h1>{{move != '' ? move : "___"}}</h1>
        </v-card-text>
        <v-card-actions class="justify-center">
            <v-btn color="secondary" :disabled="move != ''" @click="onClickButton">Select Space</v-btn>
        </v-card-actions>   
    </v-card>
</template>

<script>
export default {
    props:["move", "index"],
    data: function(){
        return{
            styleObject: {
                color: 'red',
                textalign: 'center'
            }
        }
    },
    methods:{
        //emits call, triggering player move in parent component
        onClickButton(){
            this.$emit('clicked', this.index)
        }
    },
}
</script>

<style>

</style>
<template>
    <div class="loadbar">
        <h1>Citations</h1>
        <div class="progress">
            <div class="progress-bar" role="progressbar" 
            aria-valuenow="0" 
            aria-valuemin="0" 
            aria-valuemax="100"
            :style="{
                width: (counterQuote*10) + '%'
            }">{{counterQuote}}/10</div>
        </div>
    </div>
</template>

<script>
import {eventBus} from './../main.js'

export default {
    data(){
        return{
            counterQuote: 0
        }
    },
   created() {
       eventBus.$on('quotesLength', data =>{
           this.counterQuote = data
       })
   },
}
</script>

<style scoped>
.loadbar{
    margin-top: 10px;
}
</style>

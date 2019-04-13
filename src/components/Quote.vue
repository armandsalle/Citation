<template>
    <div class="quotes row">
        <div class="quote" v-for="(quote, index) in quotes" :key="index" @click="deleteQuote(index)">
            {{quote.text}}
        </div>
        
    </div>
</template>

<script>
import {eventBus} from './../main.js'

export default {
    data(){
          return{
            quotes: [{text:'First quote', id: 0}],
            ok: true
          }
        },
    created() {
        eventBus.$emit('quotesLength', this.quotes.length)
        eventBus.$on('addQuote', data => {
            this.ok = true;

            if(this.quotes.length >= 10){
                alert('Limite de 10 citations atteinte')
            }else if(data.text === ''){
                alert('Citation vide non acceptee')
            }else{
                this.quotes.forEach(element => {
                    if(element.text === data.text){
                        alert('Citation deja prise ou citation vide')
                        this.ok = false
                    }
                })
            
                if(this.ok){
                    this.quotes.push(data)
                    eventBus.$emit('quotesLength', this.quotes.length)
                }
            }
        })
    },
    methods: {
        deleteQuote(index){
            this.quotes.splice(index, 1)
            eventBus.$emit('quotesLength', this.quotes.length)
        }
    },
}
</script>

<style scoped>
.quotes{
    display: flex;
    flex-wrap: wrap;
}

.quote{
    padding: 10px;
    border: 1px solid #223311;
    color: #223311;
    text-align: center;
    border-radius: 2px;
    margin: 10px;
    cursor: pointer;
}
</style>

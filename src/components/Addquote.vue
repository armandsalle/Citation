<template>
    <div>
        <div class="form-group">
             <label for="comment">Votre citation:</label>
            <textarea class="form-control" rows="5" id="comment" v-model="quote"></textarea>
        </div>
        <button type="button" class="btn btn-primary" @click="addQuote">Ajouter une citation</button>
        <hr>
    </div>
</template>

<script>
import {eventBus} from './../main.js'

export default {
    data(){
          return{
            quote: '',
            id: 0
          }
        },
        methods: {
          addQuote(){
              this.id++         
              eventBus.$emit('addQuote', {text: this.quote, id: this.id})
              this.quote = ''
          }
        },
}
</script>
<template>
    <div class="container">
      <app-loadbar></app-loadbar>
      <app-addquote></app-addquote>
      <app-quote></app-quote>
      <footer v-if="hasQuotes" class="col-sm-12 col-md-12 col-lg-12">
        <div class="alert alert-success">
          <strong>Clicker</strong> sur une citation pour la supprimer.
        </div>
      </footer>
    </div>
</template>

<script>
  import Quote from './components/Quote.vue'
  import Loadbar from './components/Loadbar.vue'
  import Addquote from './components/Addquote.vue'
  import {eventBus} from './main.js'

    export default {
      created() {
        eventBus.$on('quotesLength', data => {
           if(data === 0){
             this.hasQuotes = false
           }else{
             this.hasQuotes = true
           }
       })
      },
      data(){
        return {
          hasQuotes: false
        }
      },
        components: {
          appQuote: Quote,
          appLoadbar: Loadbar,
          appAddquote: Addquote
        }
    }
</script>

<style scoped>
footer{
  margin-top: 20px;
}
</style>

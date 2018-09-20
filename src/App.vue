<template>
  <div id="app" class="text-center">
    <h1>Multi translator</h1>
    <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
    <ul id="example-1">
      <li v-for="word in words">
        {{ word }}
      </li>
    </ul>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import axios from 'axios'
let url = 'https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20180918T035733Z.0403f2aa10334fc4.421d7c2af7681f545dea5c8f42b061d8dbf609f5';
export default {
  name: 'App',
  data() {
    return {
      words: []
    };
  },
  components: {
    TranslateForm
  },
  methods: {
    translateText: function (text, langHome) {
      if(text) {
        /* axios
          .post('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20180918T035733Z.0403f2aa10334fc4.421d7c2af7681f545dea5c8f42b061d8dbf609f5&lang=en-de&text=' + text)
          .then(response => {
            this.words = [];
            this.words.push( response.data.text[0])}); */

          axios.all([
            axios.get(url + '&lang=' + langHome + '-en&text=' + text),
            axios.get(url + '&lang=' + langHome + '-fr&text=' + text)
          ])
          .then(axios.spread((en, fr) => {
            this.words = []
            this.words.push( en.data.text[0])
            this.words.push( fr.data.text[0])
          }))

      }
    }
  }
}
</script>

<style>
#app {
}
</style>

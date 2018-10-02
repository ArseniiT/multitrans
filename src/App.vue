<template>
  <div id="app" class="text-center">

    <div class="container">

      <div class="row">
        <div class="col-sm"></div>
        <div class="col-sm home-box">
          <h1>Multi translator</h1>
          <TranslateForm
            v-on:formSubmit="translateText"
            v-on:langsSubmit="changeLangs"
          ></TranslateForm>
        </div>
        <div class="col-sm"></div>
      </div>

      <TranslateOutput :words="words"></TranslateOutput>

    </div>

    <FooterV></FooterV>

  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'
import FooterV from './components/FooterV'

import axios from 'axios'
let url = 'https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20180918T035733Z.0403f2aa10334fc4.421d7c2af7681f545dea5c8f42b061d8dbf609f5';
export default {
  name: 'App',
  data() {
    return {
      words: [{lang: 'en', text: ''}, {lang: 'fr', text: ''}, {lang: 'de', text: ''}],
      langs: []
    };
  },
  components: {
    TranslateForm,
    TranslateOutput,
    FooterV
  },
  methods: {
    translateText: function (text, langHome, langs) {
      if(text) {
        let promises = [];
        langs.forEach(e => {
          promises.push( axios.get(url + '&lang=' + langHome + '-' + e + '&text=' + text))
        })
        axios.all(promises)
        .then(axios.spread((...args) => {
          this.words = []
          for (let i = 0; i < args.length; i++) {
            this.words.push( {lang: args[i].data.lang.substring(3, 5), text: args[i].data.text[0]})
          }
        }))
      }
    },
    changeLangs: function (langs) {
      if(langs) {
        this.words =[]
        langs.forEach(e => {
          this.words.push( {lang: e, text: ''})
        });
      }
    }
  }
}
</script>

<style>
body {
  background-color: #f7f7f7;
}

.home-box {
  margin-top: 10px;
  background-color: #fff;
  border-radius: 5px;
  padding-bottom: 10px;
}

.result-box {
  margin-top: 30px;
}

.bg-color {
  background-color: #e7eef1 !important;
}

</style>

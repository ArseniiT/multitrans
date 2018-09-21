<template>
  <div id="app" class="text-center">

    <div class="container">

      <div class="row">
        <div class="col-sm"></div>
        <div class="col-sm home-box">
          <h1>Multi translator</h1>
          <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
          <!-- <ul id="example-1">
            <li v-for="word in words">
              {{ word }}
            </li>
          </ul> -->
        </div>
        <div class="col-sm"></div>
      </div>

      <div class="card-deck result-box">
        <div v-for="word in words" class="card">
          <img class="card-img-top flag" src="./img/de.jpg" alt="Card image cap">
          <div class="card-body">
            <h5 class="card-title">Card title</h5>
            <p class="card-text">{{word}}</p>
          </div>
        </div>

      </div>

    </div>

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
          axios.all([
            axios.get(url + '&lang=' + langHome + '-ru&text=' + text),
            axios.get(url + '&lang=' + langHome + '-en&text=' + text),
            axios.get(url + '&lang=' + langHome + '-fr&text=' + text),
            axios.get(url + '&lang=' + langHome + '-de&text=' + text)
          ])
          .then(axios.spread((en, fr, de) => {
            this.words = []
            this.words.push( en)
            this.words.push( fr.data.text[0])
            this.words.push( de.data.text[0])
          }))
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

.flag {
  height: 60px;
}


</style>

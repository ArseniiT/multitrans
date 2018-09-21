<template>
  <div id="translateForm">

          <div class="custom-block">
            <button v-on:click="choosedLang('ru')" class="btn btn-light custom">RU</button>
            <button v-on:click="choosedLang('en')" class="btn btn-light custom">ENG</button>
            <button v-on:click="choosedLang('fr')" class="btn btn-light custom">FR</button>
            <button v-on:click="choosedLang('de')" class="btn btn-light custom">DEUTSCH</button>
          </div>

          <form v-on:submit="formSubmit">
            <input type="text" class="form-control" rows="3" v-model="textForTranslate" placeholder="Enter a text" >
            <br>
            <input type="submit" class="btn btn-primary btn-lg"
            v-bind:value="'Translate from ' + langHome"
            value="Translate + 'langHome'">
          </form>

  </div>
</template>

<script>
export default {
  name: 'translateForm',
  data() {
    return{
      textForTranslate: '',
      langHome: 'ru',
      langs: ['en', 'fr', 'de']
    }
  },
  methods: {
    formSubmit (e) {
      this.$emit('formSubmit', this.textForTranslate, this.langHome, this.langs);
      e.preventDefault();
    },
    choosedLang (e) {
      this.langHome = e;
      this.langs = ['ru', 'en', 'fr', 'de']
      let index = this.langs.indexOf(e);
      if (index > -1) {
        this.langs.splice(index, 1);
      }
      this.$emit('langsSubmit', this.langs);
    }
  }
}
</script>

<style>
.custom {
    width: 78px !important;
}
.custom-block {
  margin-top: 20px;
  margin-bottom: 20px;
}

</style>

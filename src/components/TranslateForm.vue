<template>
  <div id="translateForm">

          <div class="custom-block">
            <button v-on:click="langHome = 'ru'" class="btn btn-light custom">RU</button>
            <button v-on:click="langHome = 'en'" class="btn btn-light custom">ENG</button>
            <button v-on:click="langHome = 'fr'" class="btn btn-light custom">FR</button>
            <button v-on:click="langHome = 'de'" class="btn btn-light custom">DEUTSCH</button>
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
      langHome: 'ru'
    }
  },
  methods: {
    formSubmit(e){
      this.$emit('formSubmit', this.textForTranslate, this.langHome);
      e.preventDefault();
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

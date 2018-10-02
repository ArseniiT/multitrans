<template>
  <div class="card-deck result-box">
    <div v-for="word in words" class="card shadow p-3 mb-5 bg-white rounded">
      <div :class="'flag-' + word.lang" class="shadow-sm p-3 mb-5 bg-color"><h4>{{ word.lang }}</h4></div>
      <div class="card-body">
        <p class="card-text text-success"><h2>{{ word.text }}</h2></p>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'translateOutput',
  props: ['words']
}
</script>

<style>
.flag-de {
  background: url("../img/de.jpg") no-repeat;
  background-size: auto 60px;
  height: 60px;
  background-repeat: no-repeat;
}
.flag-ru {
  background: url("../img/ru.jpg") no-repeat;
  background-size: auto 60px;
  height: 60px;
  background-repeat: no-repeat;
}
.flag-en {
  background: url("../img/en.jpg") no-repeat;
  background-size: auto 60px;
  height: 60px;
  background-repeat: no-repeat;
}
.flag-fr {
  background: url("../img/fr.jpg") no-repeat;
  background-size: auto 60px;
  height: 60px;
  background-repeat: no-repeat;
}

</style>

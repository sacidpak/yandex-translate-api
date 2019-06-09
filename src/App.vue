<template>
  <div id="app" class="container">
    <h1 class="text-center">Vue-Translator</h1>
    <br>
    <div class="row">
      <div class="col-md-12 text-center">
        <translate-form
          @translateEvent="translatedText = $event"
          @historyEvent="history.push($event)"
        ></translate-form>
        <div v-show="translatedText.length > 0" class="well">
          <h3 class="text-danger text-center">{{translatedText}}</h3>
        </div>
        <search-history v-show="history.length > 0" :history="history"></search-history>
      </div>
    </div>
  </div>
</template>

<script>
import TranslateForm from "./components/TranslateForm.vue";
import SearchHistory from "./components/SearchHistory.vue";

export default {
  name: "app",
  components: {
    TranslateForm,
    SearchHistory
  },
  data() {
    return {
      translatedText: "",
      history: []
    };
  }
};
</script>

<style>
body {
  background-color: #dedede;
}
</style>

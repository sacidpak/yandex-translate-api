<template>
  <form @submit.prevent="translateIt" class="well">
    <div class="text-left">
      <strong v-show="detectedLang.length > 0">Detected Language : {{detectedLang}}</strong> 
    </div>
    <textarea
      v-model="translateText"
      cols="30"
      rows="5"
      class="form-control"
    ></textarea>
    <br>
    <div class="text-left">
      <strong>Translate To</strong>
    </div>
    <select v-model="translateLanguage" class="form-control">
      <option v-for="(value,key) in languages" :key="key" :value="key">{{value}}</option>
    </select>
    <br>
    <button type="submit" class="btn btn-primary btn-block">Translate</button>
  </form>
</template>
<script>
import axios from "axios"
export default {
  data(){
    return {
      translateText : "",
      translateLanguage : "",
      languages : {},
      detectedLang : ""
    }
  },
  methods : {
    translateIt(){
      let url = "https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20190609T195455Z.59a049fd6df2eda4.b6abeba2cfb16d6a39430f0861414c9c7ba36674&text="+this.translateText+"&lang="+this.translateLanguage
      axios.get(url)
           .then(response => {
             this.detectedLang = this.languages[response.data.lang.split("-")[0]]
             let translatedText = response.data.text[0]
             this.$emit("translateEvent",translatedText);

             let history = {
               from : this.detectedLang,
               to : this.languages[this.translateLanguage],
               translateText : this.translateText,
               translatedText : translatedText
             }

             this.$emit("historyEvent",history)
           }).catch(ex => console.log(ex))
    }
  },
  created(){
    axios.get("https://translate.yandex.net/api/v1.5/tr.json/getLangs?key=trnsl.1.1.20190609T195455Z.59a049fd6df2eda4.b6abeba2cfb16d6a39430f0861414c9c7ba36674&ui=en")
         .then(response => {
           this.languages = response.data.langs
         })
         .catch(ex => console.log(ex))
  }
};
</script>
<style scoped>
</style>


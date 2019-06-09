<template>
  <div class="well">
    <h3>Translate History</h3>
    <ul class="list-group text-left">
      <li v-for="(item,index) in history" :key="index" class="list-group-item" style="margin-top:10px">
        <div>
          <strong>{{item.from}} >> {{item.to}}</strong>
        </div>
        <br>
        <div>
          <strong class="text-success">{{item.translateText}}</strong>
          <strong>>></strong>
          <strong class="text-danger">{{item.translatedText}}</strong>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props : ["history"]
};
</script>
<style scoped>
</style>


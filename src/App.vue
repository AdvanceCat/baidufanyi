<template>
  <div class="text-center" id="app">
    <h1>在线翻译</h1>
    <h5>Vue.js+jQuery+BaiduTransAPI</h5>
    <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'
export default {
  name: 'app',
  components: {
    TranslateForm,
    TranslateOutput
  },
  data() {
    return {
      translatedText: ''
    }
  },
  methods: {
    translateText(text) {
      var that = this;
      $.ajax({
          url: 'https://fanyi-api.baidu.com/api/trans/vip/translate',
          type: 'get',
          dataType: 'jsonp',
          data: {
              q: text[0],
              appid: text[3],
              salt: text[4],
              from: text[1],
              to: text[2],
              sign: text[5]
          },
          success: function (data) {
              that.translatedText = data['trans_result'][0]['dst'];
          }
      });
    }
  }
}
</script>

<style>
body{background-color: #fefefe;}
h1{font-size: 38px}
</style>

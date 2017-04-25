<template>
  <div id="TranslateForm">
    <form class="form-inline" v-on:submit="formSubmit">
      <input class="form-control" type="text" v-model="textToTranslate" placeholder="请输入中文...">
      <input class="btn btn-primary" type="submit" value="翻译">
    </form>
  </div>
</template>

<script>
import MD5 from 'MD5'
export default {
  name: 'TranslateForm',
  data() {
    return {
      textToTranslate: '',
      lang: '',
      appid: '20170405000044178',
      key: 'H8aMnVznGq4WGAyUuSZw',
      from: 'zh',
      to: 'en'
    }
  },
  methods: {
    formSubmit(e) {
      var salt = (new Date).getTime();
      var str = MD5(this.appid + this.textToTranslate + salt + this.key);
      this.$emit('formSubmit', [this.textToTranslate, this.from, this.to, this.appid, salt, str]);
      e.preventDefault();
    }
  }
}
</script>

<style>

</style>

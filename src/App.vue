<template>
  <div id="app">
    <h1>Word Translator</h1>
    <h5>Powered By Vue.js</h5>
    <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
    <TranslateOutput v-text="translatedText" />
  </div>
</template>

<script>
import TranslateForm from "./components/TranslateForm";
import TranslateOutput from "./components/TranslateOutput";
export default {
  name: "App",
  components: {
    TranslateForm,
    TranslateOutput
  },
  data() {
    return {
      translatedText: ""
    };
  },
  methods: {
    translateText: function(text, language) {
      this.$http
        .get(
          `https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20200517T000444Z.9a67a3947f52ccd2.3c159c1ca49786c446f872b0f32d0e74951f54b2&lang=${language}&text=${text}`
        )
        .then(res => {
          this.translatedText = res.body.text[0];
        });
    }
  }
};
</script>

<style>
#app {
  text-align: center;
}
</style>

<script setup>
import TranslateForm from '@/components/TranslateForm.vue'
import TranslateOutput from './components/TranslateOutput.vue';
import languageOptVue from './components/languageOpt.vue';
</script>

<template>
  <div id="app">
    <header>
      <img src="./assets/translate.png" alt="Logo">
      <h1>Language Translation</h1>
    </header>
    <languageOptVue v-if="showSource" @sendLanguageSource="receiverLanguagesSouce"
      @sendLanguageTarget='receiveLanguageTarget' class="languemenu" />
    <div class="translationarea">
      <!--Recibe funcion con showSource para crear el methods y abrir el menu // SendbarCode y received es el codigo del lenguaje seleccionado en la barra-->
      <TranslateForm @formSubmit="textToBeTranslated" @toggleLanguemenuSource="LangueToggleSource"
        @sendBarCode="receivedBarCode" :translation="translation(textToTranslate, languageCodeSource)"
        :languageBar="languageBar"> </TranslateForm>
      <TranslateOutput :translatedText="translatedText" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  components: {
    TranslateForm,
    TranslateOutput,
    languageOptVue
  },
  data() {
    return {
      translatedText: '',
      showSource: '',
      languageBarSelectorSource: [],
      languageBar: [{
        "language": "es",
        "name": "Spanish"
      },
      {
        "language": "en",
        "name": "English"
      },
      {
        "language": "fr",
        "name": "French"
      }],
      languageCodeSource: '',
      textToTranslate: '',
      languageCodeTarget: '',
      showTarget: '',
    }
  },
  methods: {
    textToBeTranslated(text) {
      this.textToTranslate = text

    },
    receiverLanguagesSouce(bar, languagesource, closesource, btn) {
      this.languageBarSelectorSource = bar;
      this.languageCodeSource = languagesource;
      this.showSource = closesource
      this.btnIndex = btn
      this.languageBar.unshift(this.languageBarSelectorSource)

    },

    //Recive LanguageTarget
    receiveLanguageTarget(languagetarget) {
      this.languageCodeTarget = languagetarget
      console.log('reveice', this.languageCodeTarget)
    },

    async translation(text, codeSource) {
      console.log('translateText', text, codeSource)
      const response = await fetch(`https://translation.googleapis.com/language/translate/v2?q=${text}&target=es&source=${codeSource}&model=base&key=AIzaSyCniWAIjzngaT_ZJPljhfNZwWl9VruR-kI`);
      const resdata = await response.json();
      this.translatedText = resdata.data.translations[0].translatedText
    },

    /* reveiced Menu source opener */
    LangueToggleSource(opensource) {
      this.showSource = opensource
      this.showSource = !this.showSource
    },

    receivedBarCode(langueCode) {
      this.languageCodeSource = langueCode
    },

  },

};
</script>


<style>
header {
  display: flex;
  flex-direction: row;
  justify-content: center;
  width: 100%;
  padding-top: 20px;
}

header img {
  height: 11vh;
  width: auto;
}

header h1 {
  font-family: 'Fira Sans', sans-serif;
  font-size: 2.5rem;
}

.translationarea {
  padding-top: 30px;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.languemenu {
  position: absolute;
  left: 7%;
  top: 20.1%;
}
</style>

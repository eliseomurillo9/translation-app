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
    <languageOptVue v-if="showSource" @sendLanguageSource="receiverLanguagesSouce" class="languemenu" />
    <div class="translationarea">
      <!--Recibe funcion con showSource para crear el methods y abrir el menu // SendbarCode y received es el codigo del lenguaje seleccionado en la barra-->
      <TranslateForm @formSubmit="textToBeTranslated" @toggleLanguemenu="LangueToggle" @sendBarCode="receivedBarCode" :translation="translation(textToTranslate, languageCodeSource)"
        :languageBar="languageBar"> </TranslateForm>
      <TranslateOutput v-text="translatedText"> </TranslateOutput>
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
      textToTranslate: ''
    }
  },
  methods: {
    textToBeTranslated(text) {
      this.textToTranslate = text

    },
    receiverLanguagesSouce(bar, languagesource) {
      this.languageBar = bar;
      this.languageCodeSource = languagesource;
    },

    async translation(text, codeSource) {
      console.log('translateText', text, codeSource)
      const response = await fetch(`https://translation.googleapis.com/language/translate/v2?q=${text}&target=es&source=${codeSource}&model=base&key=AIzaSyCniWAIjzngaT_ZJPljhfNZwWl9VruR-kI`);
      const resdata = await response.json();
      this.translatedText = resdata.data.translations[0].translatedText
    },
    LangueToggle(){
      this.showSource = !this.showSource
    },
    //
    receivedBarCode(langueCode){
      this.languageCodeSource = langueCode
      console.log('final', this.languageCodeSource)
    }
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

.languemenu{
  position: absolute;
  left: 6%;
  top: 23%;
}
</style>

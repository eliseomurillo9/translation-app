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
    <languageOptVue v-if="showSource" @sendLanguage="receiverLanguagesSouce" class="languemenu" />
    <languageOptVue v-if="showTarget" @sendLanguage="receiverLanguageTarget" class="languemenu" />
    <div class="translationarea">
      <!--Recibe funcion con showSource para crear el methods y abrir el menu // SendbarCode y received es el codigo del lenguaje seleccionado en la barra-->
      <TranslateForm @formSubmit="textToBeTranslated" @toggleLanguemenuSource="LangueToggleSource"
        @sendBarCode="receivedBarCode" @selectedItemSource="selectedItemSource" @resetForm="resetForm"
        :languageBar="languageBar" :activeButtonSource="activeButtonSource" :textToTranslate="textToTranslate">
      </TranslateForm>
      <TranslateOutput @ToggleListenerTarget="LangueToggleTarget" :translatedText="translatedText"
        :languageBarTarget="languageBarTarget" :activeButtonTarget="activeButtonTarget"
        @sendBarCodeTarget='receivedBarCodeTarget' @sendButtonSelected="receivedButtonSelected" />
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
      languageBarSelectorTarget: [],
      languageBar: [{
        "language": "",
        "name": "Detect Language"
      },
      {
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
      languageBarTarget: [{
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
      showTarget: null,
      showSource: null,
      activeButtonSource: null,
      activeButtonTarget: null,
    }
  },

  watch: {
        languageBar: {
            handler: function (newbar) {
                console.log('change detected');
                this.activeButtonSource = 1;
            },
            deep: true
        },

        languageBarTarget: {
            handler: function (newbar) {
                console.log('change detected');
                this.activeButtonTarget = 0;
            },
            deep: true
        }
    },

  methods: {
    async textToBeTranslated(text) {
      this.textToTranslate = text
      await this.translation(this.textToTranslate, this.languageCodeSource, this.languageCodeTarget)

    },
    receiverLanguagesSouce(bar, languagesource) {
      this.languageBarSelectorSource = bar;
      this.languageCodeSource = languagesource;
      this.languageBar.splice(1, 0, this.languageBarSelectorSource);
      this.showSource = false;
    },

    //Recive LanguageTarget
    receiverLanguageTarget(bar, languagetarget) {
      this.languageBarSelectorTarget = bar;
      this.languageCodeTarget = languagetarget;
      this.languageBarTarget.unshift(this.languageBarSelectorTarget);
      this.showTarget = false;
    },
    /* manda datos a API para traduccion */
    async translation(text, codeSource, codetarget) {
      console.log('translateText', text, codeSource, codetarget)
      const response = await fetch(`https://translation.googleapis.com/language/translate/v2?q=${text}&target=${codetarget}&source=${codeSource}&model=base&key=AIzaSyCniWAIjzngaT_ZJPljhfNZwWl9VruR-kI`);
      const resdata = await response.json();
      this.translatedText = resdata.data.translations[0].translatedText
      console.log('final', this.translatedText);
    },

    /* reveiced Menu source opener */
    LangueToggleSource() {
      this.showSource = !this.showSource
    },

    receivedBarCode(langueCode) {
      this.languageCodeSource = langueCode
    },
    /* Listener para el boton de target */
    LangueToggleTarget() {
      this.showTarget = !this.showTarget
    },

    /*Received bar code from target*/
    receivedBarCodeTarget(languagecodebartg) {
      this.languageCodeTarget = languagecodebartg
    },
    /*selector style un language bar*/
    selectedItemSource(i) {
      this.activeButtonSource = i
      console.log('It Works', i);
    },

    receivedButtonSelected(i) {
      this.activeButtonTarget = i
    },

    resetForm() {
      this.textToTranslate = '';
      this.translatedText = '';
      console.log('i worked')
    }
  },

};
</script>


<style>
header {
  display: flex;
  justify-content: center;
  padding-top: 20px;
}

header img {
  height: 10vh;
  align-self: center;
  margin-left: 4px;
}

header h1 {
  font-family: 'Fira Sans', sans-serif;
  font-size: 2.5rem;
  align-self: center;
  margin-top: 8px;
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
  left: 6%;
  top: 19.2%;
}

@media screen and (max-width: 900px) {
  .translationarea {
    color: aqua;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
  }

  @media screen and (max-width: 500px) {
    header h1 {
      text-align: center;
      width: 150px;
      font-size: 1.6rem;
    }
  }
}
</style>

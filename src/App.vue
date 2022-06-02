<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from '@/components/HelloWorld.vue'
import TranslateForm from '@/components/TranslateForm.vue'
import TranslateOutput from './components/TranslateOutput.vue';
import { onMounted } from '@vue/runtime-core';
</script>

<template>
  <div id="app">
    <header>
    <img src="./assets/translate.png" alt="Logo">
    <h1>Language Translation</h1>
    </header>
    <div class="translationarea">
    <TranslateForm @formSubmit="translateText"> </TranslateForm>
    <TranslateOutput v-text="translatedText"> </TranslateOutput>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  components: {
    TranslateForm,
    TranslateOutput
  },
  data() {
    return {
      translatedText: '',
    }
  },
  methods: {
    async translateText(text) {
      const response = await fetch(`https://translation.googleapis.com/language/translate/v2?q=${text}&target=es&source=en&model=base&key=AIzaSyCniWAIjzngaT_ZJPljhfNZwWl9VruR-kI`);
      const resdata = await response.json();
      this.translatedText = resdata.data.translations[0].translatedText;
      
    },
  },
}




</script>
<style>

header{
  display: flex;
  flex-direction: row;
  justify-content: center;
  width: 100%;
  padding-top: 20px;
}
header img{
  height: 11vh;
  width: auto;
}

header h1{
  font-family: 'Fira Sans', sans-serif;
  font-size: 2.5rem;
}

.translationarea{
  padding-top: 30px;
  width: 100%;
  height: 100%;
}
</style>

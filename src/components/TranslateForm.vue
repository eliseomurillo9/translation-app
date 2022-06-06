
<template>
    <div id="translateForm">
        <language-opt v-if="showLanguageList" :languageCodeSource="languageCodeSource"></language-opt>
        <div class="box">
            <div v-for="(languages, i) in languageBar" :key="i">
                <input type="button" :value="languages.name" />
            </div>
        </div>
        <form @submit="formSubmit">

            <textarea v-model="textToTranslate" ref="textarea" rows="1" @input="resize($event)">
  </textarea>
            <input type="submit" value="Translate">

        </form>


    </div>
</template>

<script>
import languageOpt from './languageOpt.vue';

export default {
    components: { languageOpt },
    props: ['languageCodeSource'],
    name: 'translateForm',
    setup() {
        return {
            textToTranslate: '',
            showLanguageList: false,
            languageCodeSource: '',
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
            }]
        }
    },

    methods: {
        formSubmit(e) {
            this.$emit('formSubmit', this.textToTranslate, this.languageCodeSource);
            e.preventDefault();
        },

        resize(e) {
            e.target.style.height = 'auto',
                e.target.style.height = `${e.target.scrollHeight}px`
        }

    },

}
</script>

<style>
.box {
    background-color: aqua;
    display: flex;
    flex-direction: row;
    justify-content: left;
    width: 40vw
}

.box input{
    cursor: pointer;
    background: none;
    border: none;
}

form {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-content: center;
    align-items: center;
}

form :nth-child(1) {
    border-radius: 5px;
    width: 40vw;
    min-height: 20vh;
    border: none;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
    outline: none;
}

input {
    height: 25px;
}
</style>
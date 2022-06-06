<template>
    <div id="languageOpt">
        <div class="list-div">
            <div v-for="(langue, i) in languesList" :key="i" class="list">
                <input type="button" :value="langue.name" @click="selectLanguage(langue.language)" />
            </div>
        </div>
    </div>

</template>


<script>
import { onMounted } from 'vue'

export default {

    data() {
        return {
            languesList: [],
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
        selectLanguage(langues) {
            this.languageCodeSource = langues
        }
    },

    async mounted() {
        const res = await fetch('https://translation.googleapis.com/language/translate/v2/languages?target=en&key=AIzaSyCniWAIjzngaT_ZJPljhfNZwWl9VruR-kI');
        const langdata = await res.json();
        const list = langdata.data.languages.forEach(element => {
            return this.languesList.push(element)
        })
    }

}
</script>

<style>
#LanguageOpt{
    width: 50vw;
    height: 100wh;
}

.list-div{
    background-color: #ffff;
    box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px, rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-content: center;
    width: auto;
    height: auto;
    padding: 20px 0 20px 0;
}

.list-div .list{
    display: flex;
    justify-content: center;
    align-content: center;
}

.list-div input{
    background: none;
    color: inherit;
    border: none;
    font: inherit;
	cursor: pointer;
	outline: inherit;
    text-align: center;
    width: 150px;
    height: auto;
    font-family: fira sans;
    font-weight: 400;
    margin: 5px 10px 5px 10px;
    transition: ease-in-out;
    border-radius: 15px;
}

.list-div input:hover{
    background-color: rgba(194, 190, 190, 0.5)
}
</style>
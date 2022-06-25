<template>
    <div id="languageOpt">
        <div class="list-div">
            <div v-for="(langue, i) in languesList" :key="i" class="list">
                <input type="button" :value="langue.name" @click="selectLanguage(langue)" />
            </div>
        </div>
    </div>

</template>


<script>
export default {

    data() {
        return {
            languesList: [],
            languageCode: '',
            languageBarSelectorSource: '',
        }
    },

    methods: {
        selectLanguage(langues) {
            /* Send Language source */
                this.languageCode = langues.language;
                this.languageBarSelectorSource = langues;
                this.$emit('sendLanguage', this.languageBarSelectorSource, this.languageCode)
               
        }
    },

    async mounted() {
        const res = await fetch('https://translation.googleapis.com/language/translate/v2/languages?target=en&key=AIzaSyCniWAIjzngaT_ZJPljhfNZwWl9VruR-kI');
        const langdata = await res.json();
        const list = langdata.data.languages.forEach(element => {

            return this.languesList.push(element)
        })
    }

};


</script>

<style>
.list-div {
    background-color: #ffff;
    box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-content: center;
    width: 86vw;
    height: auto;
    padding: 20px 0 20px 0;
    border-radius: 5px;
}

.list-div .list {
    display: flex;
    justify-content: center;
    align-content: center;
}

.list-div input {
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

.list-div input:hover {
    background-color: rgba(194, 190, 190, 0.5)
}
</style>
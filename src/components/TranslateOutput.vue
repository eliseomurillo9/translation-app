<template>
    <div id="TranslateOutPut">
        <div class="box">
            <div v-for="(languages, i) in languageBarTarget.slice(0, 3)" :key="i"
                @click="langueBarSelector(languages.language, i)" :class="{ btnselected: i === activeButtonTarget }">
                <input type="button" :value="languages.name" @click="selectItemT(i)" />
            </div>
            <img src="../assets/downchevron_85745.png" alt="Menu" @click="toggleListenerTarget">
        </div>
        <div class="translation">
            <p>{{ translatedText }}</p>
        </div>

    </div>
</template>

<script>
export default {
    props: ['translatedText', 'languageBarTarget', 'activeButtonTarget'],
    name: 'TranslateOutput',
    setup() {
        return {
            showTarget: false,
            
        }
    },


    methods: {
        toggleListenerTarget() {
            this.$emit('ToggleListenerTarget')
        },

        langueBarSelector(languecode) {
            console.log(languecode)
            this.$emit('sendBarCodeTarget', languecode)
        },

        /*color blue in language selected*/
        selectItemT(i) {
            this.activeBtn = i
            this.$emit('sendButtonSelected', i)
        }

    }
}
</script>

<style>
#TranslateOutPut {
    display: flex;
    flex-direction: column;
    align-content: center;
    background-color: #ffff;
    border-radius: 5px;
    width: 40vw;
    min-height: 20vh;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
}

.translation {
    font-family: fira sans;
    font-weight: 400;
    font-size: 18px;
    padding-top: 5px;
}

.translation p {
    margin: 0 10px 0 10px;
}

.btnselected input {
    font-size: 20px;
    font-weight: 700;
    color: rgb(61, 158, 227);

}

@media screen and (max-width: 900px){
    #TranslateOutPut{
        margin: auto;
        width: 100vw;
        min-height: 25vh;
    }

    .box{
        width: 100vw;
    }
}
</style>
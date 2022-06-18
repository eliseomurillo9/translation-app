<template>
    <div id="TranslateOutPut">
        <div class="box">
            <div>
                <input type="button" value="English" />
                <input type="button" value="Spanish" />
                <input type="button" value="French" />
            </div>
            <img src="../assets/downchevron_85745.png" alt="Menu" @click="toggleListenerTarget">
        </div>
        <div class="translation">
            <p>hole como estas</p>
        </div>

    </div>
</template>

<script>
export default {
    name: 'TranslateOutput',
    props: ['translatedText'],

     setup() {
        return {
            showTarget: false,
        }
    },

    methods: {
      
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

.translation p{
    margin: 0 10px 0 10px;
}
</style>
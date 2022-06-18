
<template>
    <div id="translateForm">
        <div class="box">
            <input type="button" value="Detect Language" />
            <!--langueBarSelector toma el codigo de lenguaje de la barra para enviarlo a app-->
            <div v-for="(languages, i) in languageBar.slice(0, 3)" :key="i" @click="langueBarSelector(languages.language, i)"
                :class="{ btnselected: i === activeBtn }">
                <input type="button" :value="languages.name" @click="selectItem(i)" />
            </div>
            <img src="../assets/downchevron_85745.png" alt="Menu" @click="toggleListener">
        </div>
        <form @submit="formSubmit2">

            <textarea v-model="textToTranslate" ref="textarea" rows="1" @input="resize($event)">
  </textarea>
            <input type="submit" value="Translate">

        </form>


    </div>
</template>

<script>
export default {
    props: ['languageBar'],
    name: 'translateForm',

    watch: {
        languageBar: {
            handler: function (newbar) {
                console.log('change detected');
                     this.activeBtn = 0;
            },
            deep: true
        }
    },

    setup() {
        return {
            textToTranslate: '',
            showSource: false,
            activeBtn: null,
        }
    },


    methods: {

        formSubmit2(e) {
            this.$emit('formSubmit', this.textToTranslate);
            e.preventDefault();
        },

        resize(e) {
            e.target.style.height = 'auto',
                e.target.style.height = `${e.target.scrollHeight}px`
        },
        //Enviar toggle para abrir menu de idiomas
        toggleListener() {
            this.$emit('toggleLanguemenuSource', this.showSource)
        },
        //Envia codigo de lenguaje a app
        langueBarSelector(languecode) {
            console.log(languecode)
            this.$emit('sendBarCode', languecode)
            //this.colorbtn = true
        },
        selectItem(i) {
            this.activeBtn = i
            console.log(this.activeBtn)
        }
    },

}
</script>

<style>
.box {
    background-color: rgb(255, 255, 255);
    display: flex;
    flex-direction: row;
    justify-content: left;
    align-items: center;
    width: 40vw;
    height: 35px;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
    box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px;
    border-bottom: 0.3px solid;
    border-bottom-color: rgba(168, 168, 168, 0.5);
}

.box input {
    cursor: pointer;
    background: none;
    border: none;
    margin-left: 6px;
    font-size: 18px;
    color: rgb(71, 71, 71);
    padding: 0 8px 0 8px;
    border-radius: 5px;
}

.box input:hover {
    background-color: rgba(194, 190, 190, 0.5);
    color: black;
}

.btnselected input {
    font-size: 20px;
    font-weight: 700;
    color: rgb(61, 158, 227);

}

.box img {
    height: 13px;
    cursor: pointer;
    border-radius: 25px;
}

.box img:hover {
    background-color: rgba(194, 190, 190, 0.5);
}

form {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-content: center;
    align-items: center;
}

form :nth-child(1) {
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
    width: 40vw;
    min-height: 20vh;
    border: none;
    outline: none;
}

form textarea {
    box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px -1px, rgba(0, 0, 0, 0.06) 0px 2px 4px -1px;
    font-family: fira sans;
    font-weight: 400;
    font-size: 18px;
    padding-top: 5px;
}

form input {
    height: 25px;
    cursor: pointer;
    border: none;
    border-radius: 9px;
    background-color: rgb(61, 158, 227);
    color: white;
    padding: 6px;
    margin: 0 10px 0 10px;
    font-family: fira sans;
    font-weight: 600;
    font-size: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
    transition: ease-in-out, 0.3s;

}

form input:hover {
    background-color: rgb(23, 158, 255);
    color: #fff;

}
</style>
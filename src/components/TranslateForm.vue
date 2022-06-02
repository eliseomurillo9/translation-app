<template>
    <div id="translateForm">
        <form @submit="formSubmit">
            <textarea v-model="textToTranslate" ref="textarea" rows="1" @input="resize($event)">
  </textarea>
            <input type="submit" value="Translate">
        </form>
    </div>
</template>

<script>
export default {
    name: 'translateForm',
    setup() {
        return {
            textToTranslate: '',
        }
    },

    methods: {
        formSubmit(e) {
            this.$emit('formSubmit', this.textToTranslate);
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
form :nth-child(1) {
    border-radius: 5px;
    width: 40vw;
    min-height: 20vh;
    border: none;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
    outline: none;
}
</style>
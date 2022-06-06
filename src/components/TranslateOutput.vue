<template>
    <div id="TranslateOutPut">
            <p>{{ translatedText }}</p>
    </div>
</template>

<script>
export default {
    name: 'TranslateOutput',
    props: ['translatedText'],
}
</script>

<style>
#TranslateOutPut {
    background-color: #ffff;
    border-radius: 5px;
    width: 40vw;
    min-height: 20vh;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
}
</style>
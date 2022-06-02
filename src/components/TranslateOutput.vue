<template>
    <div id="TranslateOutPut">
        <div class="translatedspace">
            <p>{{ translatedText }}</p>
        </div>

    </div>
</template>

<script>
export default {
    name: 'TranslateOutput',
    props: ['translatedText'],
}
</script>

<style>
.translatedspace {
    background-color: rgb(0, 0, 0);
    border-radius: 5px;
    width: 40vw;
    min-height: 20vh;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
}
</style>
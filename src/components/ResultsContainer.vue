<template>
    <div class="results-container" >
        <h2 class="results-container__title">Your Inspiration:</h2>
        <div v-show="loading" class="spinner">
            Generating...
        </div>
        <div v-show="loaded" class="results-image">
            <img :src="inspirationUrl" >
        </div>
        <recirc-container
            v-show="loaded"
            :selectedRoom="selectedRoom"
            :selectedTags="selectedTags" />
    </div>
</template>

<script>
import RecircContainer from './Recirc.vue'

export default {
    name: "ResultsContainer",
    props: ["inspirationUrl", "loading", "loaded", "selectedRoom", "selectedTags"],
    components: {
        RecircContainer
    }
}
</script>

<style>

.results-container {
    padding: 3rem 0 0;

}

.results-container__title {
    margin-bottom: 2rem;
}
</style>


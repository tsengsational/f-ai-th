<template>
    <div class="results-container" >
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


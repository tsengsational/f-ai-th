<template>
    <div class="results-container">
        <div class="results-image">
            <img :src="inspiration" >
        </div>
    </div>
</template>

<script>

export default {
    name: "ResultsContainer",
    props: ["inspiration"]
}
</script>


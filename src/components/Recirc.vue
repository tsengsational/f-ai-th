<template>
    <div class="interior-desaign__recirc">
        <h2 v-show="showRecirc">More inspirations:</h2>
        <div
            v-show="showRecirc"
            v-for="(article, index) in filteredArticles"
            :key="index"
            class="interior-desaign__recirt-article">
            <div class="recirc-article__image-container">
                <img :src="article['Primary Image']" />
            </div>
            <h3 class="recirc-article__title">
                <a class="recirc-article__link" :href="article.Url">{{ article.Title }}</a>
            </h3>
        </div>
    </div>
</template>

<script>
import dummyData from './DummyData'

export default {
    name: "RecircContainer",
    props: ["selectedRoom", "selectedTags"],
    data() {
        return {
            articles: dummyData
        }
    },
    computed: {
        filteredArticles() {
            return dummyData.filter( article => article.Room == this.selectedRoom)
        },
        showRecirc() {
            return this.filteredArticles.length > 0;
        }
    }
}
</script>

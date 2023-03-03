<template>
    <form class="design-form">
        <div class="design-form__room-type">
            <span class="design-form__room-text">
                I'm designing a
            </span>
            <select v-model="selectedRoom" >
                <option v-for="(room, index) in alphaRooms" :key="index">{{ room }}</option>
            </select>
        </div>
        <fieldset class="design-form__room-tags">
            <legend class="design-form__room-tags-legend">Select your vibes:</legend>
            <div class="design-form__room-tags-list">
                <div class="design-form__room-tags-list-item" v-for="(tag, index) in tags" :key="index">
                    <label :for="tag">
                        <input type="checkbox" :name="tag" :value="tag" v-model="selectedTags">
                        <span>{{ tag }}</span>
                    </label>
                </div>
            </div>
        </fieldset>
        <button
            @click.prevent="submitPrompt(textPrompt, selectedRoom, selectedTags)"
            :disabled="isDisabled">
            Generate
        </button>
        <a href="#" @click.prevent="reset" >Reset</a>
    </form>
</template>

<script>

export default {
    name: "DesignForm",
    props: ["submitPrompt"],
    data() {
        return {
            rooms: ["Kitchen", "Living Room", "Bed Room", "Study", "Bath Room", "Dining Room", "Entry Way", "Teen Girls Room", "Teen Boys Room", "Kids Room", "Nursery", "Home Office", "Home Library", "Balcony", "Patio", "Vanity Room"],
            tags: ["Bohemian", "Concrete", "Minimalist", "Maximalist", "Midcentury", "Grandmillennial", "Traditional", "Japandi", "Scandinavian", "European", "Mediterranian", "Victorian", "Serious", "Playful", "Vibrant", "Organic", "Farmhouse", "Classic", "Luxurious", "Japanese", "Feng Shui", "Vintage", "Contemporary", "Industrial", "Monochromatic"],
            selectedRoom: null,
            selectedTags: [],
            prompt: null
        }
    },
    computed: {
        alphaRooms() {
            return this.alphaSort(this.rooms)
        },
        alphaTags() {
            return this.alphaSort(this.tags)
        },
        isDisabled() {
            return !this.selectedRoom;
        },
        textPrompt() {
            return `magazine spread photograph of a ${this.selectedRoom} with ${this.selectedTags.join(", ")} style, high def, atmospheric lighiting, dynamic lighting`
        }
    },
    methods: {
        alphaSort(arr) {
            return [...arr].sort((a, b) => {
                if (a < b) {
                    return -1;
                }
                if (a > b) {
                    return 1;
                }
                return 0;
            })
        },
        reset(){
            this.selectedRoom = null;
            this.selectedTags = []
            this.$emit('resetForm')
        },
        toggleTag(event) {
            const tag = event.target.value;
            if (this.selectedTags.includes(tag)) {
                this.selectedTags = this.selectedTags.filter( el => el !== tag );
            } else {
                this.selectedTags.push(tag);
            }
        },
    }
}
</script>

<style>
.design-form__room-text {
    font-weight: bold;
}

.design-form__room-tags {
    border: none;
    margin: 2rem 0;
}

.design-form__room-tags-legend {
    font-weight: bold;
    text-align: left;
}

.design-form__room-tags-list-item label input {margin-right: 100px;}

.design-form__room-tags-list-item {
    margin: 4px;
    background-color: #104068;
    border-radius: 4px;
    border: 1px solid #fff;
    overflow: hidden;
    float: left;
}

.design-form__room-tags-list-item label {
    float: left; line-height: 3.0em;
    width: 8.0em; height: 3.0em;
}

.design-form__room-tags-list-item label span {
    text-align: center;
    padding: 3px 0;
    display: block;
}

.design-form__room-tags-list-item label input {
    clip: rect(0 0 0 0);
    clip-path: inset(50%);
    height: 1px;
    overflow: hidden;
    position: absolute;
    white-space: nowrap;
    width: 1px;
}

.design-form__room-tags-list-item label input + span {
    color: #fff;
}

.design-form__room-tags-list-item input:checked + span {
    color: #ffffff;
    text-shadow: 0 0  6px rgba(0, 0, 0, 0.8);
}

.action input:checked + span {
    background-color: #F75A1B;
}
</style>

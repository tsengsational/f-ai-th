<template>
    <form class="design-form">
        <div class="design-form__room-type">
            <span class="design-form__room-text">
                I'm designing a
            </span>
            <select v-model="selectedType">
                <option v-for="(room, index) in alphatype" :key="index">{{room}}</option>
            </select>
        </div>
        <fieldset class="design-form__room-tags">
            <legend class="design-form__room-tags-legend">Select your moods:</legend>
            <div class="design-form__room-tags-list">
                <div class="design-form__room-tags-list-item" v-for="(tag, index) in tags" :key="index">
                    <input type="checkbox" :name="tag" :value="tag" :id="tag" v-model="selectedTags">
                    <label :for="tag">
                        <span>{{tag}}</span>
                    </label>
                </div>
            </div>
        </fieldset>
        <div class="design-form__button-wrapper">
            <button
                class="design-form__button-submit"
                @click.prevent="submitPrompt(textPrompt, selectedType, selectedTags)"
                :disabled="isDisabled">
                Generate
            </button>
            <div class="design-form__button-reset-wrapper">
                <a href="#" @click.prevent="reset" class="design-form__button-reset">Reset</a>
            </div>
        </div>
    </form>
</template>

<script>

    export default {
        name: "DesignForm",
        props: ["submitPrompt"],
        data() {
            return {
                type: ["Chocolate", "Pastry", "Cake", "Drink", "Hard Candy", "Caramel", "Nougat", "Cookie", "Chip", "Pretzel", "Nuts", "Fruit"],
                tags: ["Sugar-coated", "Crisp", "Light", "Heavy", "Sour", "Bright", "Creamy", "Buttery", "Firey", "Icey"],
                selectedType: null,
                selectedTags: [],
                prompt: null
            }
        },
        computed: {
            alphaType() {
                return this.alphaSort(this.type)
            },
            alphaTags() {
                return this.alphaSort(this.tags)
            },
            isDisabled() {
                return !this.selectedType;
            },
            textPrompt() {
                return `magazine spread photograph of a ${this.selectedType} snack food with ${this.selectedTags.join(", ")} style, high def, atmospheric lighiting, dynamic lighting`
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
            reset() {
                this.selectedType = null;
                this.selectedTags = []
                this.$emit('resetForm')
            },
            toggleTag(event) {
                const tag = event.target.value;
                if (this.selectedTags.includes(tag)) {
                    this.selectedTags = this.selectedTags.filter(el => el !== tag);
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

    .design-form__room-tags-list-item {
        margin: 4px;
        color: #000;
        font-weight: bold;
        border-radius: 8px;
        overflow: hidden;
        float: left;
    }

    .design-form__room-tags-list {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
    }

    .design-form__room-tags-list-item label {
        line-height: 3.0em;
        width: 8.0em;
        height: 3.0em;
        background-color: #dcde7d;
        display: inline-block;

    }

    .design-form__room-tags-list-item input + label:hover {
        background-color: #a8de7d;
    }

    .design-form__room-tags-list-item input:checked + label {
        background-color: #a8de7d;
    }

    .design-form__room-tags-list-item input:checked + label:hover {
        background-color: #72c068;
    }

    .design-form__room-tags-list-item label span {
        text-align: center;
        padding: 3px 0;
        display: block;
    }

    .design-form__room-tags-list-item input {
        clip: rect(0 0 0 0);
        clip-path: inset(50%);
        height: 1px;
        overflow: hidden;
        position: absolute;
        white-space: nowrap;
        width: 1px;
    }

    .design-form__button-wrapper {
        text-align: center;
    }

    .design-form__button-submit {
        background-color: #5bad4d;
        border-radius: 4px;
        border: none;
        color: #FFF;
        font-weight: bold;
        padding: 1rem 2rem;
        text-transform: uppercase;
        font-size: 1.25rem;
        cursor: pointer;
    }

    .design-form__button-submit:hover {
        background-color: #348425;
        transition: background-color .3s;
    }

    .design-form__button-submit:disabled {
        background-color:#aaaaaa;
        color: #2c3e50;
        cursor: auto;
    }

    .design-form__button-reset-wrapper {
        margin-top: 1rem;
    }

    .design-form__button-reset {
        color: #000;
        font-weight: bold;
    }

    .design-form__button-reset-wrapper {
        text-align: right;
        padding-right: 2rem;
    }
</style>

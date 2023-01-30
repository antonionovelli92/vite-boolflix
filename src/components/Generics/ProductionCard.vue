<script>
import { pics } from '../../data';
export default {
    name: 'ProductionCard',
    data() {
        pics
    },
    props: {
        item: Object,
    },
    computed: {
        title() {
            return this.item.title || this.item.name
        },
        originalTitle() {
            return this.item.original_title || this.item.original_name
        },
        hasFlag() {
            const flags = ['it', 'en'];
            return flags.includes(this.item.original_language)
        },
        flagSrc() {
            const url = new URL(`../../assets/img/${this.item.original_language}.png`, import.meta.url)
            return url.href;
        },
        posterPath() {
            if (!this.item.poster_path) return pics.placeholder;
            return pics.baseUrl + this.item.poster_path;
        },
        vote() {
            return Math.ceil(this.item.vote_average / 2)
        }
    },
    methods: {
        setStarClass(n) {
            return n <= this.vote ? 'fa-solid' : 'fa-regular';
        }
    }
};
</script>

<template>
    <div class="poster d-flex  container">
        <div class=" d-flex flex-direction-row ">
            <div class=" cinema ">
                <ul>
                    <li>{{ title }}</li>
                    <li>{{ originalTitle }}</li>
                    <li>
                        <img v-if="hasFlag" :src="flagSrc" :alt="item.original_language" class="flag">
                        <div v-else>{{ item.original_language }}</div>
                    </li>
                    <li>
                        <img class="cover" :src="posterPath" :alt="title">
                    </li>
                    <li>
                        <i v-for="n in 5" :class="setStarClass(n)" class="fa-star"></i>
                    </li>
                </ul>
            </div>
        </div>


    </div>

</template>

<style scoped lang="scss">
.poster {
    flex-basis: 33%;
    background-color: rgba(31, 29, 29, 0.417);



    .cinema {
        min-width: 100%;
        min-height: 300px;
    }

    ul {

        margin-bottom: 1rem;
        justify-content: center;
        text-align: center;
        max-width: 100%;

        li {
            list-style: none;
            display: flex;

            .flag {
                max-width: 100%;
                height: 12px;
            }

            .cover {


                display: inline-block;
            }
        }
    }


}
</style>
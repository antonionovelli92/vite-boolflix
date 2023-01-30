<script>
import ProductionCard from './ProductionCard.vue';
import { store } from '../../data/store';
export default {
    name: 'ProductionSection',
    components: { ProductionCard },
    props: {
        title: String,
        collection: String
    },
    data() {
        return { store }
    }
}
</script>

<template>
    <section :id="collection">
        <h2>{{ title }}</h2>
        <production-card v-for="production in store[collection]" :key="production.id"
            :item="production"></production-card>
    </section>
</template>

<style scoped lang="scss">
section {}
</style>
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
section {
    background-color: rgba(66, 65, 65, 0.213);
    border: 25px;
    flex-direction: row;
    display: flex;
    overflow-y: auto;

}
</style>
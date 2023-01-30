<script>
import ProductionSection from './Generics/ProductionSection.vue';
export default {
    name: 'AppMain',
    components: { ProductionSection },
}
</script>

<template>
    <main>
        <production-section collection="movies" title="Movies"></production-section>
        <production-section collection="series" title="TV Series"></production-section>

    </main>
</template>

<style>

</style>
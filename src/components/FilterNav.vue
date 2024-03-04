<template>
    <div class="filterNav">
        <button @click="filterBy('all')" :class="{active: current === 'all'}" >All</button>
        <button @click="filterBy('ongoing')" :class="{active: current === 'ongoing'}" >Ongoing</button>
        <button @click="filterBy('completed')" :class="{active: current === 'completed'}" >Completed</button>
    </div>
</template>

<script>
    export default {
        name: 'FilterNav',
        props: ["current"],
        methods: {
            filterBy(value) {
                this.$emit('FilterValue', value);
            }
        },
    }
</script>

<style>

</style>
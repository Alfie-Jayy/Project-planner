<template>
    <div class="singleProject">
        <div>
            <h1 class="font-bold text-green-500 pb-3  cursor-pointer "  @click="showDeatail=!showDeatail" >{{ project.title }}</h1>
            <h3 v-if="showDeatail" class="text-md text-gray-600 font-semibold" >{{ project.detail }}</h3>
        </div>
        <div class="space-x-5" >
            <i class="fa-solid fa-trash single-icon" @click="deleteProject"></i>
            <i class="fa-solid fa-pen single-icon"></i>
            <i class="fa-solid fa-check single-icon"></i>
        </div>
    </div>
</template>

<script>
    import axios from "axios"
    export default {
        props: ['project'],
        data() {
            return {
                showDeatail: false,
            }
        },
        methods: {
            deleteProject() {
                axios.delete(`http://localhost:3000/projects/${this.project.id}`).then((result) => {
                    this.$emit('delete', this.project.id)
                }).catch((err) => {
                    console.log(err);
                });
            }
        },
    }
</script>

<style>

</style>
<template>
    <div class="navbar">
        <router-link to="/" >Projects</router-link>
        <router-link :to="{name: 'addProject'}" >Add Project</router-link>
    </div>
</template>

<script>
    export default {
        name: 'Nav'
    }
</script>



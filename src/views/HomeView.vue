<template>
  <div class="home">
    <h1 class="text-start text-blue-500 text-xl font-bold py-10 px-10">Home</h1>
    <div v-for="project in projects" :key="project.id">
      <SingleProject :project="project"></SingleProject>
    </div>
  </div>
</template>

<script>

import SingleProject from '../components/SingleProject'
import axios from "axios";
export default {
  name: 'HomeView',
  components: {
    SingleProject,},
  data() {
    return {
      projects: []
    }
  },
  mounted () {
    axios.get('http://localhost:3000/projects').then((result) => {
      this.projects = result.data
    }).catch((err) => {
      console.log(err);
    });
  },
}
</script>

<template>
  <div class="home">
    <h1 class="text-start text-blue-500 text-xl font-bold pt-10 ms-10">Home</h1>
    <div v-for="project in projects" :key="project.id">
      <SingleProject :project="project" @delete="deleteProject" ></SingleProject>
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

  methods: {
    deleteProject(id) {
      this.projects =  this.projects.filter((project) => {
        return project.id != id
      })
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

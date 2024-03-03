<template>
  <div class="main">    
    <div v-for="project in projects" :key="project.id">
      <SingleProject :project="project" @delete="deleteProject" @complete="completeProject" ></SingleProject>
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
    },

    completeProject(id){
      let findProject = this.projects.find((project) => {
        return project.id === id
      })
      findProject.complete = !findProject.complete
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

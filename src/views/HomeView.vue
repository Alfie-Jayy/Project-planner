<template>
  <div class="main">    
    
    <FilterNav @FilterValue="current=$event" :current="current" ></FilterNav>

    <div v-for="project in filterProjects" :key="project.id">
      <SingleProject :project="project" @delete="deleteProject" @complete="completeProject" ></SingleProject>
    </div>

  </div>
</template>

<script>

import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
import axios from "axios";
export default {
  name: 'HomeView',
  components: {
    FilterNav,
    SingleProject,},
  data() {
    return {
      projects: [],
      current: "all"
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

  computed: {
    filterProjects() {
      
      if(this.current === 'ongoing'){
        return this.projects.filter((p)=>{
          return !p.complete
        })
      }
      else if(this.current === 'completed'){
        return this.projects.filter((p)=>{
          return p.complete
        })
      }
      else{
        return this.projects
      }

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

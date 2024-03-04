<template>
  <div class="singleProject" :class="{ complete: project.complete }">
    <div>
      <h1
        class="font-bold text-sky-500 cursor-pointer"
        @click="showDeatail = !showDeatail"
      >
        {{ project.title }}
      </h1>
      <h3 v-if="showDeatail" class="text-md text-gray-600 pt-3 font-semibold">
        {{ project.detail }}
      </h3>
    </div>
    <div class="space-x-5">
      <i class="fa-solid fa-trash single-icon" @click="deleteProject"></i>
      <router-link :to="{name:'editProject', params: {id: project.id} }">
        <i class="fa-solid fa-pen single-icon"></i>
      </router-link>
      <i class="fa-solid fa-check single-icon" @click="completeProject"></i>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["project"],
  data() {
    return {
      showDeatail: false,
      api: "http://localhost:3000/projects/",
    };
  },
  methods: {
    deleteProject() {
      axios
        .delete(`http://localhost:3000/projects/${this.project.id}`)
        .then((result) => {
          this.$emit("delete", this.project.id);
        })
        .catch((err) => {
          console.log(err);
        });
    },

    //fetch
    completeProject() {
      const updateRoute = this.api + this.project.id;

      const headers = {
        "Content-Type": "application/json",
      };

      const body = JSON.stringify({ complete: !this.project.complete });

      fetch(updateRoute, { method: "PATCH", headers, body })
        .then((response) => {
          this.$emit("complete", this.project.id);
        })
        .catch((error) => {
          console.error(error);
        });
    },

    //axios
    // completeProject() {

    //     const updateRoute = this.api + this.project.id;

    //     const body = {
    //         complete: !this.project.complete,
    //     };

    //     axios.patch(updateRoute, body)

    //     .then((response) => {
    //         this.$emit("update", this.project.id);
    //     })
    //     .catch((error) => {
    //         console.error(error);
    //     });
    // }
  },
};
</script>

<style></style>

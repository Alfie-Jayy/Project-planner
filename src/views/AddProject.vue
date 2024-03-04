<template>
    <div class="main">
        
        <form @submit.prevent="AddProject" >        
                <div>
                    <label class="label" for="">Project title</label>
                    <input class="input" type="text" v-model="title" >
                    <span v-if="titleError" class="titleError" >Project title field is required!</span>
                </div>

                <div>
                    <label class="label" for="">Project detail</label>
                    <input class="input" type="text" v-model="detail" >
                    <span v-if="detailError" class="detailError">Project detail field is required!</span>
                </div>

                <div class="text-center">
                    <button class="btn" type="submit">Add Project</button>
                </div>
        
        </form>
    
    </div>
</template>

<script>
import axios from 'axios'
    export default {
        
        name: 'AddProject',
        
        data() {
            return {
                title: "",
                detail: "",
                titleError: false,
                detailError: false
            }
        },
        
        methods: {
            AddProject() {
            
                if (this.title === "") {
                    this.titleError = true
                } else {
                    this.titleError = false
                }

                if (this.detail === "") {
                    this.detailError = true
                } else {
                    this.detailError = false
                }

                if(this.title && this.detail){
                    
                    axios({
                        method:'post',
                        url: "http://localhost:3000/projects",
                        data: {
                            "title" : this.title,
                            "detail": this.detail,
                            "complete": false
                        }
                    }).then(() => {
                        //redirect
                        this.$router.push('/')
                    }).catch((err) => {
                        console.log(err);
                    });
                
                }
            
            }
        },
    }
</script>

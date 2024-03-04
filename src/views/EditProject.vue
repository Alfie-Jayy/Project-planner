<template>
    <div class="main">
        <form @submit.prevent="UpdateProject" >        
                <div>
                    <label class="label">Project title</label>
                    <input class="input" type="text" v-model="title" >
                    <span v-if="titleError" class="titleError" >Project title field is required!</span>
                </div>

                <div>
                    <label class="label">Project detail</label>
                    <input class="input" type="text" v-model="detail" >
                    <span v-if="detailError" class="detailError">Project detail field is required!</span>
                </div>

                <div class="text-center">
                    <button class="btn" type="submit">Update Project</button>
                </div>
        
        </form>
    </div>
</template>

<script>
import axios from "axios";
    export default {
        
        name: 'EditProject',
        props: ["id"],
        
        data() {
            return {          
                title: "",
                detail: "",
                titleError: false,
                detailError: false
            }
        },

        methods: {
            UpdateProject() {
            
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
                    
                    
                    axios.patch(`http://localhost:3000/projects/${this.id}`, {
                        title: this.title,
                        detail: this.detail
                    })

                    .then(() => {
                        //redirect
                        this.$router.push('/')
                    }).catch((err) => {
                        console.log(err);
                    });
                
                }
            
            }
        },
        
        mounted () {
            
            axios.get(`http://localhost:3000/projects/${this.id}`)
            
            .then(result => {
                this.title = result.data.title,
                this.detail = result.data.detail
            })
            .catch(err => {
                console.error(err); 
            });
            
        },
    }
</script>


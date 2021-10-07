<template>
    <div>
    <h1>Home Feed</h1>
        <v-textarea
            outlined
            clearable
            name="input-7-4"
            label="Create A Post"
            v-model="postInput"
        ></v-textarea>
        <v-textarea
            outlined
            clearable
            name="input-7-4"
            label="Enter Username"
            v-model="usernameInput"
        ></v-textarea>
        <v-textarea
            outlined
            clearable
            name="input-7-4"
            label="Enter Date YYYY-MM-DD"
            v-model="dateInput"
        ></v-textarea>
        <v-btn
            @click="post_content()"
            color="primary"
            elevation="2"
            raised
        >Submit</v-btn>
        <p id="confirmResponse"></p>
        <FeedPost
            v-for="post in allPosts"
            v-bind:key="post.id"
            :content="post.content"
            :username="post.username"
            :time_created="post.time_created"
            />
    </div>
</template>

<script>
import axios from "axios";
import FeedPost from "./FeedPost.vue"
    export default {
        name : "Feed",
        components: {
            FeedPost
        },
        data(){
            return{
                postInput: "",
                usernameInput: "",
                dateInput : "",
                allPosts : []
            }
        },
        mounted () {
        },
        methods: {
            post_content() {
                axios.request({
                    url : "http://127.0.0.1:5000/api/feed",
                    method : "POST",
                    headers : {
                        'Content-Type': 'application/json'
                    },
                    data : {
                        "content" : this.postInput,
                        "username" : this.usernameInput,
                        "time_created" : this.dateInput
                    }
                }).then((response) => {
                    console.log(response);
                    document.getElementById('confirmResponse').innerText="Post Created"
                }).catch((error) => {
                    console.error("There was an error" +error);

                })

            },
        }

    }
</script>

<style scoped>

</style>
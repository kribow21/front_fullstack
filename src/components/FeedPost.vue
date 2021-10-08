<template>
    <div>
        <v-card
        class="mx-auto"
        color="primary"
        dark
        max-width="100%"
        >
        <v-card-title>
            <v-list-item-content>
                <v-list-item-title>
                    <v-card-title>{{username}}</v-card-title>
                    <p>{{time_created}}</p>
                </v-list-item-title>
            </v-list-item-content>
            <v-icon
                small
                left
                >
                mdi-twitter
            </v-icon>
        </v-card-title>
            <v-card-text class="text-h5 font-weight-bold">
                {{content}}
            </v-card-text>
        <v-card-actions>
        <v-list-item class="grow">
            <v-row
                align="center"
                justify="end"
            >
                <!-- form for editing post-->
                <v-icon @click="clickToEdit" class="mr-1"
                color="accent">
                mdi-comment-edit-outline
                </v-icon>
                        <div :class="{EditForm : isForm}">
                        <v-col
                            cols="12"
                            sm="10"
                        >
                        <v-text-field
                            label="edited post"
                            v-model="editedContent"
                            outlined
                        ></v-text-field>
                        <v-btn
                                @click="editPost"
                                color="primary"
                                elevation="2"
                                raised
                            >Apply</v-btn>
                            
                        </v-col>
                        </div>
                <v-icon @click="deletePost" class="mr-1"
                color="accent">
                mdi-comment-remove-outline
                </v-icon>
            </v-row>
            </v-list-item>
        </v-card-actions>
    </v-card>
    </div>
</template>

<script>
import axios from "axios";
    export default {
        name : 'FeedPost',
            props : {
                id : Number,
                content : String,
                username : String,
                time_created : String
    },
    data() {
        return {
            editedContent: "",
            isForm: true,

        }
    },
    methods: {
    clickToEdit(){
        if (this.isForm == true){
            this.isForm = false
        }else if(this.isForm == false){
            this.isForm = true
        }
    },
    editPost(){
        console.log(this.editedContent)
        console.log(this.id)
        axios.request({
            url : "https://kbfirstfullstack.ml/api/feed",
            method : "PATCH",
            headers : {
                'Content-Type': 'application/json'
            },
            data : {
                "content" : this.editedContent,
                "id" : this.id
            }
        }).then((response) => {
        print(response)
        console.log(response);
        this.$emit('UpdateFeed');


        }).catch((error) => {
            console.error("There was an error" +error);
        })
    },
        deletePost(){
        axios.request({
            url : "https://kbfirstfullstack.ml/api/feed",
            method : "DELETE",
            headers : {
                'Content-Type': 'application/json'
            },
            data : {
                "id" : this.id
            }
        }).then((response) => {
        print(response)
        console.log(response);
        this.$emit('DeletePostFromFeed');

        }).catch((error) => {
            console.error("There was an error" +error);
        })
    }
    }

    }

</script>

<style scoped>
.EditForm{
    display: none;
}
</style>
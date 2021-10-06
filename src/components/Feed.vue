<template>
    <div>
        <h1>Home Feed</h1>
        <v-textarea
            outlined
            clearable
            name="input-7-4"
            label="Create A Post"
            v-model="tweetInput"
        ></v-textarea>
        <v-btn
            color="primary"
            elevation="2"
            raised
        >Tweet</v-btn>
        <FeedPost></FeedPost>
    </div>
</template>

<script>
import FeedPost from "./FeedPost.vue"
    export default {
        name : "Feed",
        components: {
            FeedPost
        }
    }
</script>

<style scoped>

</style>
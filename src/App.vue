<template>
    <div id="app">
        <v-container>
                <v-row>
                    <v-col cols="12" sm="3" xs="6">
                        <h1>My Posts</h1>
                    </v-col>
                    <v-col cols="12" sm="9" xs="6">                    
                        <NewPost v-on:add-post="submitPost"/>
                    </v-col>
                </v-row>
            <Posts v-bind:posts="posts" v-on:del-post="deletePost" v-on:edit-post="editPost"/>
        <v-snackbar
            v-model="snackbar"
            :timeout="2000"
            >
            <span>{{snackbarText}}</span>
        </v-snackbar>
        </v-container>
    </div>
</template>

<script>
    import Posts from './components/Posts';
    import NewPost from './components/NewPost';
    import axios from 'axios';

    export default {
        name: 'app',
        components: {
            Posts,
            NewPost
        },
        data() {
            return {
                posts: [],
                snackbar: false,
                snackbarText: ''
            }
        },
        methods: {
            deletePost(id) {
                axios.delete(`https://jsonplaceholder.typicode.com/posts/${id}`)
                    .then(() => {
                        this.posts = this.posts .filter(post => post.id !== id);
                    })
                    .catch(() => {
                        this.snackbar = true
                        this.snackbarText = "Sorry, this post cannot be deleted"
                    })
            },
            submitPost(newPost) {
                const {title, body, userId} = newPost;
                axios.post('https://jsonplaceholder.typicode.com/users/1/posts', {
                    title,
                    body,
                    userId
                })
                .then(res => {
                    this.posts = [res.data, ...this.posts]
                })
                .catch(() => {
                    this.snackbar = true;
                    this.snackbarText = "Something went wrong adding this post"
                })
            },
            editPost(updatedPost) {
                axios.put(`https://jsonplaceholder.typicode.com/posts/${updatedPost.id}`, updatedPost)
                .then(res => {
                    const postIndex = this.posts.findIndex(post => post.id == updatedPost.id);
                    const newPosts = this.posts;
                    newPosts[postIndex] = res.data;
                    this.posts = Object.assign([], this.posts, newPosts);
                })
                .catch(() => {
                    this.snackbar = true
                    this.snackbarText = "Sorry, this post cannot be edited"
                })
            }
        },
        created() {
            axios.get('https://jsonplaceholder.typicode.com/users/1/posts')
                .then(res => this.posts = res.data)
                .catch(() => {
                    this.snackbar = true
                    this.snackbarText = "Something went wrong fetching your posts"
                })
        }
    }
</script>

<style>
    body {
        font-family: Roboto, sans-serif;
    }
</style>

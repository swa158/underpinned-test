<template>
    <div id="app">
        <v-container>
            <h2>My Posts</h2>
            <NewPost v-on:add-post="submitPost"/>
            <Posts v-bind:posts="posts" v-on:del-post="deletePost"/>
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
                posts: []
            }
        },
        methods: {
            deletePost(id) {
                axios.delete(`https://jsonplaceholder.typicode.com/users/1/posts/${id}`)
                    .then(res => console.log(res))
            },
            submitPost(newPost) {
                const {title, body} = newPost;
                axios.post('https://jsonplaceholder.typicode.com/users/1/posts', {
                    title,
                    body
                })
                    .then(res => {
                        this.posts = [res.data, ...this.posts]
                    })
                // .catch(err => )   //todo put toast here
            }
        },
        created() {
            axios.get('https://jsonplaceholder.typicode.com/users/1/posts')
                .then(res => this.posts = res.data)
                // .catch(err => )   //todo put toast here
        }
    }
</script>

<style>
    /** {*/
        /*box-sizing: border-box;*/
        /*margin: 0;*/
        /*padding: 0;*/
    /*}*/
    body {
        font-family: Roboto, sans-serif;
    }
</style>

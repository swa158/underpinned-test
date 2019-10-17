<template>
    <div>
        <v-container>
            <v-row>
                <v-col>
                    <h2>My Posts</h2>
                </v-col>
                <v-col>
                    <NewPost/>
                </v-col>
            </v-row>
            <v-layout row wrap>
                <v-flex xs12 sm6 md4 lg3
                        v-for="post in posts"
                        v-bind:key="post.id"
                >
                    <v-container>
                        <Post v-bind:post="post" v-on:del-post="$emit('del-post', post.id)"/>
                    </v-container>
                </v-flex>
            </v-layout>
        </v-container>
    </div>
</template>

<script>
    import Post from './Post';
    import NewPost from './NewPost';
    export default {
        name: 'Posts',
        components: {
            Post,
            NewPost
        },
        props: ['posts']
    }
</script>

<style scoped>

</style>
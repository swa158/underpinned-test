<template>
    <div>
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
    </div>
</template>

<script>
    import Post from './Post';

    export default {
        name: 'Posts',
        components: {
            Post
        },
        props: ['posts']
    }
</script>

<style scoped>

</style>
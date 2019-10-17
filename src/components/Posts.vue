<template>
    <div>
        <div v-for="post in posts" v-bind:key="post.id">
            <Post v-bind:post="post"/>
        </div>
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
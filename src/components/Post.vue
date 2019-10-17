<template>
    <v-card
            color="#385F73"
            dark
    >
        <v-card-title class="headline">{{post.title}}</v-card-title>

        <v-card-subtitle
                class="d-inline-block text-truncate"
            >
                {{post.body}}
        </v-card-subtitle>

        <v-card-actions>
            <v-btn @click="$emit('del-post', post.id)" text>Delete</v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
    export default {
        name: 'Post',
        props: ['post']
    }
</script>

<style scoped>

</style>
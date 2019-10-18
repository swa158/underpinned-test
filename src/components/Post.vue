<template>
    <v-card color="#f37061" dark>
        <v-card-title class="headline">{{post.title}}</v-card-title>
        <v-card-subtitle class="d-inline-block text-truncate">{{post.body}}</v-card-subtitle>
        <v-card-actions>
            <v-dialog v-model="dialog" width="500">
                <template v-slot:activator="{ on }">
                    <v-btn color="red lighten-2" dark outlined v-on="on">Delete</v-btn>
                </template>
                <v-card>
                    <v-card-title class="headline grey lighten-2" primary-title>Are you sure you want to delete this post?</v-card-title>
                    <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn color="primary" text @click="dialog = false">No</v-btn>
                        <v-btn color="secondary" text @click="$emit('del-post', post.id); dialog = false">Yes</v-btn>
                    </v-card-actions>
                </v-card>
            </v-dialog>
            <EditPost v-bind:post="post" v-on:edit-post="editPost"/>
        </v-card-actions>
    </v-card>

</template>

<script>
    import EditPost from './EditPost'
    export default {
        name: "Post",
        components: {
            EditPost
        },
        props: ["post"],
        data () {
            return {
                dialog: false
            }
        },
        methods: {
            editPost(updatedPost) {
                this.$emit('edit-post', updatedPost);
            }
        }
    };
</script>
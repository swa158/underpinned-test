<template>
    <div>
        <v-dialog v-model="dialog" width="500">
            <template v-slot:activator="{ on }">
                <v-btn color="red lighten-2" outlined v-on="on">Edit</v-btn>
            </template>
            <v-card>
                <v-card-title class="headline grey lighten-2" primary-title>Edit post</v-card-title>
                <v-form ref="form">
                    <v-card-text>
                        <v-container>
                            <v-row>
                                <v-col cols="12">
                                    <v-text-field
                                            label="Title"
                                            v-model="title"
                                            :rules="inputRules"
                                            name="title"
                                            value="title"
                                            required>
                                    </v-text-field>
                                </v-col>
                                <v-col cols="12">
                                    <v-textarea
                                            filled
                                            label="Enter description"
                                            v-model="description"
                                            :rules="inputRules"
                                            name="description"
                                            value="description"
                                            required>
                                    </v-textarea>
                                </v-col>
                            </v-row>
                        </v-container>
                    </v-card-text>
                    <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn color="blue darken-1" text @click=closeDialog()>Close</v-btn>
                        <v-btn color="blue darken-1" text @click=editPost()>Save</v-btn>
                    </v-card-actions>
                </v-form>
            </v-card>
        </v-dialog>
    </div>
</template>

<script>
    export default {
        name: "EditPost",
        props: ["post"],
        data() {
            return {
                title: this.post.title,
                description: this.post.body,
                inputRules: [
                    v => !!v || 'Field cannot be empty'
                ],
                dialog: false,
            }
        },
        methods: {
            editPost() {
                if(this.$refs.form.validate()) {
                    const updatedPost = {
                        userId: this.post.userId,
                        id: this.post.id,
                        title: this.title,
                        body: this.description
                    };
                    this.$emit('edit-post', updatedPost);
                    this.dialog = false;
                }
            },
            closeDialog() {
                this.title = '';
                this.description = '';
                this.dialog = false;
            }
        }
    }
</script>
<template>
    <div>
        <v-dialog v-model="dialog" width="500">
        <template v-slot:activator="{ on }">
          <v-btn color="red lighten-2" outlined v-on="on">Add</v-btn>
        </template>

        <v-card>
            <v-card-title class="headline grey lighten-2" primary-title>Add new post</v-card-title>

          <v-form ref="form">
            <v-card-text>
            <v-container>
                <v-row>
                <v-col cols="12">
                    <v-text-field label="Title" v-model="title" :rules="inputRules" name="title" required></v-text-field>
                </v-col>
                <v-col cols="12">
                    <v-textarea filled label="Enter description" v-model="description" :rules="inputRules" name="description" required></v-textarea>
                </v-col>
                </v-row>
            </v-container>
            </v-card-text>

            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click=closeDialog()>Close</v-btn>
                <v-btn color="blue darken-1" text @click=addPost()>Save</v-btn>
            </v-card-actions>
            </v-form>
        </v-card>
      </v-dialog>
    </div>
</template>

<script>
    export default {
        name: "NewPost",
        data() {
            return {
                title: '',
                description: '',
                dialog: false,
                inputRules: [
                    v => !!v || 'Field cannot be empty'
                ],
            }
        },
        methods: {
            addPost() {
                if(this.$refs.form.validate()) {
                    const newPost = {
                        userId: 1,  // Since there is no authentication
                        title: this.title,
                        body: this.description
                    };
                    this.$emit('add-post', newPost);
                    this.title = '';
                    this.description = '';
                    this.dialog = false;     // todo only close if it's successful
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
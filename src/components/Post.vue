<template>
  <v-card color="#f37061" dark>
    <v-card-title class="headline">{{post.title}}</v-card-title>

    <v-card-subtitle class="d-inline-block text-truncate">{{post.body}}</v-card-subtitle>

    <v-card-actions>
      <v-dialog v-model="dialogDelete" width="500">
        <template v-slot:activator="{ on }">
          <v-btn color="red lighten-2" dark outlined v-on="on">Delete</v-btn>
        </template>

        <v-card>
          <v-card-title class="headline grey lighten-2" primary-title>Are you sure you want to delete this post?</v-card-title>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" text @click="dialogDelete = false">No</v-btn>
            <v-btn color="secondary" text @click="$emit('del-post', post.id); dialogDelete = false">Yes</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <!-- <v-btn @click="$emit('edit-post', post.id)" text>Edit</v-btn> -->
      <v-dialog v-model="dialogEdit" width="500">
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
                <v-btn color="blue darken-1" text @click=editPost()>Save</v-btn>
            </v-card-actions>
            </v-form>
        </v-card>
      </v-dialog>
    </v-card-actions>
  </v-card>

</template>

<script>

// import EditPost from './EditPost'

export default {
  name: "Post",
  components: {
    //   EditPost
  },
  props: ["post"],
  data () {
      return {
        dialogDelete: false,
        dialogEdit: false,
        title: this.post.title,
        description: this.post.body,
        inputRules: [
            v => !!v || 'Field cannot be empty'
        ],
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
                this.dialogEdit = false;     // todo only close if it's successful
            }
        },
        closeDialog() {
            this.title = this.post.title;
            this.description = this.post.body;
            this.dialogEdit = false;
        }
    }
};
</script>

<style scoped>
</style>
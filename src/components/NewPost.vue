<template>
    <div>
        <form @submit="addPost">
            <input type="text" v-model="title" name="title" placeholder="Title">
            <input type="text" v-model="description" name="description" placeholder="Description">
            <input type="submit" value="Add" class="btn">
        </form>
    </div>
</template>

<script>
    export default {
        name: "NewPost",
        data() {
            return {
                title: '',
                description: ''
            }
        },
        methods: {
            addPost(e) {
                e.preventDefault();
                const newPost = {
                    userId: 1,  // Since there is no authentication
                    title: this.title,
                    body: this.description
                };
                this.$emit('add-post', newPost);
                this.title = '';
                this.description = '';
            }
        }
    }
</script>
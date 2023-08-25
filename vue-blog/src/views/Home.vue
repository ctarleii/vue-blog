<template>
    <div class="home">
        <h1>Home</h1>
        <div v-if="error">{{ error }}</div>
        <PostList :posts="posts"/>
    </div>
</template>

<script>

import {ref} from "vue";
import PostList from '../components/PostList.vue'

export default {
    name: 'Home',
    components: {
        PostList,
    },
    setup() {
        const posts = ref([])
        const error = ref(null)

        const load = async () => {
            try {
                let data = await fetch('http://localhost:3000/posts')
                if (!data.ok) {
                    throw Error('no data avaliable')
                }
                posts.value = await data.json()
            } catch (err) {
                error.value = err.message
                console.log(err.message)
            }
        }

        load()

        return {
            posts,
            error,
        }
    },

}
</script>

<script setup>
    import { ref, reactive, onMounted } from 'vue'

    let comments = reactive({ comments: [] });

    onMounted(() => {
        let api_url = "https://lab5-p379.onrender.com/api/v1/messages/";
        fetch(api_url)
            .then(response => response.json())
            .then(data => {
                comments.comments = data;
            });
    });
</script>

<template>
    <div class="videoComments">
        <h3>Comments</h3>
        <ul>
            <li v-for="comments in comments.comments" :key="comments.id">
                <p>{{ comments.user }}</p>
                <p>{{ comments.text }}</p>
            </li>
        </ul>
    </div>
</template>

<style scoped>
    div{
        padding: 0 1rem;
        height: 80vh;
    }
</style>
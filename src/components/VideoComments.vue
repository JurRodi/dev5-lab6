<script setup>
    import { ref, reactive, onMounted } from 'vue'

    let comments = reactive({ comments: [] });

    onMounted(() => {
        let api_url = "https://lab5-p379.onrender.com/api/v1/messages/";
        fetch(api_url)
            .then(response => response.json())
            .then(data => {
                comments.comments = data;
                comments.comments.reverse();
            });
    });

    const addComment = () => {
        let api_url = "https://lab5-p379.onrender.com/api/v1/messages/";
        let data = {
            "id": "",
            "user": "Anonymous",
            "text": document.querySelector(".comment").value
        }
        fetch(api_url, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        })
        .then(response => response.json())
        .then(data => {
            comments.comments.unshift(data.data);
        });
    }
</script>

<template>
    <div class="videoComments">
        <h3>Comments</h3>
        <input type="text" v-model="text" placeholder="Typ something" class="comment">
        <button @click="addComment">Add comment</button>
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
        overflow-y: scroll;
    }
</style>
<script setup>
    import { ref, reactive, onMounted } from 'vue'

    let username = ref('');
    let description = ref('');

    onMounted(() => {
        let api_url = "https://app.fakejson.com/q/MqAtrcgD?token=AR4rfmauSfMqhaWv7wTauQ";
        fetch(api_url)
            .then(response => response.json())
            .then(data => {
                username.value = data.videos[0].username;
                description.value = data.videos[0].description;
            });
    });
</script>

<template>
  <div class="videoDetails">
    <h3>{{ username }}</h3>
    <p>{{ description }}</p>
  </div>
</template>

<style scoped>
    div{
        padding: 0 1rem;
        height: 20vh;
    }
</style>

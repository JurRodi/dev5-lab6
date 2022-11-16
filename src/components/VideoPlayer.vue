<script setup>
    import { ref, reactive, onMounted } from 'vue'
    import 'animate.css'

    let src = ref('');
    let videos = reactive({ videos: [] });
    let animation = ref('');

    onMounted(() => {
        let api_url = "https://app.fakejson.com/q/MqAtrcgD?token=AR4rfmauSfMqhaWv7wTauQ";
        fetch(api_url)
            .then(response => response.json())
            .then(data => {
                src.value = data.videos[0].video;
                videos.videos = data.videos;
            });
    });

    const nextVideo = () => {
        animation.value = 'animate__fadeOut';
        setTimeout(() => {
            src.value = videos.videos[1].video;
            animation.value = 'animate__fadeIn';
        }, 1000);
    }
</script>

<template>
  <div class="video">
    <div class="controls">
        <a @click.prevent="nextVideo" href="#" class="controls__next">⬇️</a>
    </div>
    <video :src="src" type="video/mp4" controls autoplay muted class="animate__animated" :class="animation"></video>
  </div>
</template>

<style scoped>
    .video{
        width: 100%;
    }
    .controls{
        position: absolute;
        top: 0;
        left: 0;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        z-index: 1;
    }
    a{
        text-decoration: none;
    }
    video{
        width: 100%;
        max-height: 100vh;
    }
</style>